<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сайт Советской империи</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
            min-height: 100vh;
            background: #0a0a0a;
            background-image: 
                linear-gradient(180deg, 
                    #000000 0%, #000000 33.33%, 
                    #FFD700 33.33%, #FFD700 66.66%, 
                    #FFFFFF 66.66%, #FFFFFF 100%);
            background-size: 100% 100vh;
            background-repeat: no-repeat;
            background-attachment: fixed;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            position: relative;
        }

        body::before {
            content: "⚜️";
            position: fixed;
            font-size: 35rem;
            color: rgba(255, 215, 0, 0.05);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            pointer-events: none;
            font-family: 'Arial', sans-serif;
        }

        .overlay {
            width: 100%;
            max-width: 1200px;
            height: 90vh;
            max-height: 800px;
            background: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(4px);
            -webkit-backdrop-filter: blur(4px);
            border-radius: 40px;
            padding: 2rem 2.2rem;
            box-shadow: 0 20px 40px rgba(0,0,0,0.7), 0 0 0 2px #FFD700, 0 0 0 4px #1a1a1a;
            border: 1px solid #d4af37;
            transition: all 0.2s;
            display: flex;
            flex-direction: column;
        }

        .header {
            display: flex;
            align-items: center;
            gap: 24px;
            flex-wrap: wrap;
            border-bottom: 2px solid #d4af37;
            padding-bottom: 1.2rem;
            margin-bottom: 1.8rem;
            flex-shrink: 0;
        }

        .flag-container {
            flex-shrink: 0;
            width: 130px;
            height: 75px;
            border-radius: 10px;
            overflow: hidden;
            border: 2px solid #d4af37;
            box-shadow: 0 4px 12px rgba(0,0,0,0.6);
            display: flex;
            flex-direction: column;
        }

        .flag-stripe {
            flex: 1;
            width: 100%;
        }

        .flag-stripe.black {
            background: #000000;
        }
        .flag-stripe.yellow {
            background: #FFD700;
        }
        .flag-stripe.white {
            background: #FFFFFF;
        }

        .title {
            font-size: 2.6rem;
            font-weight: 700;
            letter-spacing: 4px;
            color: #f5e7d3;
            text-shadow: 0 4px 14px #000000cc, 0 0 10px #d4af37aa;
            font-family: 'Times New Roman', serif;
            flex: 1;
        }

        .title small {
            font-size: 1rem;
            font-weight: 300;
            letter-spacing: 6px;
            display: block;
            color: #e6d5b8;
            margin-top: 4px;
            text-shadow: 0 2px 6px black;
        }

        .nav-row {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 1.5rem;
            justify-content: center;
            flex-shrink: 0;
        }

        .nav-btn {
            flex: 1 0 auto;
            min-width: 120px;
            padding: 0.8rem 1.6rem;
            background: rgba(30, 25, 20, 0.7);
            backdrop-filter: blur(2px);
            border: 1px solid #d4af37;
            border-radius: 60px;
            color: #f5e7d3;
            font-size: 1.1rem;
            font-weight: 500;
            letter-spacing: 1.5px;
            text-align: center;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            font-family: 'Segoe UI', sans-serif;
            white-space: nowrap;
            user-select: none;
        }

        .nav-btn:hover {
            background: rgba(60, 45, 35, 0.8);
            border-color: #e6c14f;
            transform: scale(1.02);
            box-shadow: 0 0 20px #d4af3755;
        }

        .nav-btn.active {
            background: #d4af37;
            color: #1a1a1a;
            border-color: #f5e7d3;
            box-shadow: 0 0 30px #d4af3766;
        }

        .content-area {
            flex: 1;
            background: rgba(30, 25, 20, 0.5);
            border-radius: 28px;
            border: 1px solid #d4af37;
            padding: 2rem;
            overflow-y: auto;
            min-height: 200px;
            position: relative;
        }

        .content-area::-webkit-scrollbar {
            width: 8px;
        }

        .content-area::-webkit-scrollbar-track {
            background: rgba(30, 25, 20, 0.3);
            border-radius: 10px;
        }

        .content-area::-webkit-scrollbar-thumb {
            background: #d4af37;
            border-radius: 10px;
        }

        .section-content {
            display: none;
            height: 100%;
            color: #f0e6da;
        }

        .section-content.active {
            display: block;
        }

        .section-content h2 {
            font-family: 'Times New Roman', serif;
            font-weight: 700;
            font-size: 2rem;
            color: #f5e2c9;
            border-bottom: 2px solid #d4af37;
            padding-bottom: 0.8rem;
            margin-bottom: 1.5rem;
            letter-spacing: 2px;
            text-shadow: 0 2px 6px #000000aa;
        }

        .section-content h3 {
            font-family: 'Times New Roman', serif;
            font-size: 1.3rem;
            color: #f5d742;
            margin: 1.2rem 0 0.8rem 0;
            letter-spacing: 1px;
        }

        .section-content p {
            font-size: 1.05rem;
            line-height: 1.8;
            color: #e2d4c2;
            margin-bottom: 0.8rem;
        }

        .section-content ul {
            list-style: none;
            padding-left: 0;
        }

        .section-content ul li {
            padding: 0.4rem 0 0.4rem 2.2rem;
            position: relative;
            border-bottom: 1px dotted #4d3a2b;
            font-size: 1rem;
            line-height: 1.6;
        }

        .section-content ul li::before {
            content: "⚜️";
            position: absolute;
            left: 0;
            color: #d4af37;
            font-size: 1rem;
        }

        .section-content .rule-item {
            background: rgba(0, 0, 0, 0.25);
            border-left: 3px solid #d4af37;
            padding: 0.8rem 1.2rem;
            border-radius: 8px;
            margin-bottom: 0.8rem;
        }

        .section-content .rule-item p {
            margin-bottom: 0.3rem;
        }

        .section-content .rule-number {
            color: #f5d742;
            font-weight: 600;
        }

        .news-item {
            background: rgba(0, 0, 0, 0.3);
            border-left: 4px solid #d4af37;
            padding: 1rem 1.2rem;
            border-radius: 12px;
            margin-bottom: 1rem;
        }

        .news-item strong {
            color: #f5d742;
            font-weight: 600;
        }

        .empty-message {
            opacity: 0.7;
            font-style: italic;
            color: #c7b7a2;
        }

        .password-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(8px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .password-overlay.show {
            display: flex;
        }

        .password-modal {
            background: #1a1510;
            border: 2px solid #d4af37;
            border-radius: 32px;
            padding: 2.5rem 3rem;
            max-width: 420px;
            width: 90%;
            box-shadow: 0 0 60px rgba(212, 175, 55, 0.2);
            text-align: center;
        }

        .password-modal h3 {
            color: #f5e2c9;
            font-family: 'Times New Roman', serif;
            font-size: 1.6rem;
            margin-bottom: 0.5rem;
            letter-spacing: 2px;
        }

        .password-modal p {
            color: #c7b7a2;
            font-size: 1rem;
            margin-bottom: 1.5rem;
        }

        .password-modal input {
            width: 100%;
            padding: 0.9rem 1.2rem;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid #d4af37;
            border-radius: 60px;
            color: #f5e7d3;
            font-size: 1.1rem;
            outline: none;
            transition: 0.2s;
            text-align: center;
            letter-spacing: 4px;
        }

        .password-modal input:focus {
            border-color: #f5e7d3;
            box-shadow: 0 0 20px #d4af3755;
        }

        .password-modal .btn-group {
            display: flex;
            gap: 12px;
            margin-top: 1.5rem;
            justify-content: center;
        }

        .password-modal .btn-group button {
            padding: 0.7rem 2rem;
            border-radius: 60px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: 0.2s;
            border: 1px solid #d4af37;
            background: transparent;
            color: #f5e7d3;
            min-width: 100px;
        }

        .password-modal .btn-group button:hover {
            background: #d4af37;
            color: #1a1a1a;
        }

        .password-modal .btn-group button.cancel {
            border-color: #5a4a3a;
            color: #8a7a6a;
        }

        .password-modal .btn-group button.cancel:hover {
            background: #3a2a1a;
            color: #c7b7a2;
            border-color: #5a4a3a;
        }

        .password-error {
            color: #ff6b4a;
            font-size: 0.9rem;
            margin-top: 0.8rem;
            display: none;
        }

        .password-error.show {
            display: block;
        }

        @media (max-width: 900px) {
            .overlay {
                height: 92vh;
                max-height: none;
                padding: 1.2rem;
            }
            .title {
                font-size: 2rem;
            }
            .flag-container {
                width: 100px;
                height: 58px;
            }
            .nav-btn {
                white-space: normal;
                min-width: 80px;
                padding: 0.6rem 1rem;
                font-size: 0.95rem;
            }
            .content-area {
                padding: 1.2rem;
            }
            .section-content h2 {
                font-size: 1.6rem;
            }
            .password-modal {
                padding: 2rem 1.5rem;
            }
        }

        @media (max-width: 550px) {
            .header {
                flex-direction: column;
                align-items: flex-start;
                gap: 12px;
            }
            .title {
                font-size: 1.6rem;
            }
            .title small {
                font-size: 0.8rem;
                letter-spacing: 3px;
            }
            .nav-btn {
                min-width: 60px;
                font-size: 0.85rem;
                padding: 0.5rem 0.8rem;
            }
            .content-area {
                padding: 0.8rem;
            }
            .section-content h2 {
                font-size: 1.3rem;
            }
            .section-content p {
                font-size: 0.95rem;
            }
            .password-modal {
                padding: 1.5rem 1rem;
            }
            .password-modal h3 {
                font-size: 1.3rem;
            }
        }

        .ornament {
            text-align: center;
            color: #d4af37;
            letter-spacing: 6px;
            font-size: 0.8rem;
            margin-top: 1rem;
            opacity: 0.7;
            flex-shrink: 0;
        }
    </style>
</head>
<body>
    <div class="overlay">

        <header class="header">
            <div class="flag-container">
                <div class="flag-stripe black"></div>
                <div class="flag-stripe yellow"></div>
                <div class="flag-stripe white"></div>
            </div>
            <div class="title">
                Сайт Советской империи
                <small>⚜️ Самодержавие · Православие · Народность ⚜️</small>
            </div>
        </header>

        <div class="nav-row">
            <button class="nav-btn active" data-section="rules">📜 Правила</button>
            <button class="nav-btn" data-section="news">📰 Свежие новости</button>
            <button class="nav-btn" data-section="property">🏛️ Имущество</button>
            <button class="nav-btn" data-section="government" id="governmentBtn">🏛️ Информация для правительства</button>
        </div>

        <div class="content-area">

            <!-- ПРАВИЛА -->
            <div class="section-content active" id="section-rules">
                <h2>📜 Кодекс правил Советской Империи</h2>
                
                <h3>1. Выкуп имущества</h3>
                
                <div class="rule-item">
                    <p><span class="rule-number">1.</span> При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если же договор был составлен и подписан и покупатель решил отменить сделку, то он должен выплатить государству компенсацию в размере <strong>50 000 (д) рублей</strong>, в случае отмены сделки государством, государство не должно выплачивать компенсацию (подробнее в статье 1.2).</p>
                </div>

                <div class="rule-item">
                    <p><span class="rule-number">1.1.</span> Отменить договор можно при согласии всех членов правительства в течение <strong>1 дня</strong> на мелкую сделку и <strong>2 дней</strong> на крупную сделку.</p>
                </div>

                <div class="rule-item">
                    <p><span class="rule-number">1.2.</span> Если налоговой службе не понравится происхождение денег, выплаченных покупателем, то государство может отменить сделку (подробнее в статье 1.1.) и <strong>не выплачивать компенсацию</strong> покупателю. Государство может забрать эти деньги и вообще не отдавать их покупателю.</p>
                </div>

                <h3>2. Нарушения на дороге</h3>

                <div class="rule-item">
                    <p><span class="rule-number">2.</span> Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</p>
                    <ul>
                        <li><strong>В первый раз</strong> — обязан выплатить штраф <strong>10 рублей</strong></li>
                        <li><strong>Во второй и следующие разы</strong> — выплачивает штраф и лишается свободы на срок <strong>1 день</strong></li>
                    </ul>
                    <p style="margin-top: 0.5rem; font-style: italic; color: #c7b7a2;">*При лишении свободы деятельность человека прекращается на указанный срок.</p>
                </div>

                <div class="rule-item">
                    <p><span class="rule-number">3.</span> При ДТП на дороге все участники обязаны выплатить штраф по <strong>5 рублей</strong> с каждого:</p>
                    <ul>
                        <li><strong>Без пострадавших</strong> — штраф 5 рублей с каждого участника</li>
                        <li><strong>С пострадавшими</strong> — обвиняемый обязан выплатить помимо обязательного штрафа ещё компенсацию <strong>5 рублей</strong> государству и <strong>5 рублей</strong> пострадавшему (всего 15 рублей)</li>
                    </ul>
                </div>
            </div>

            <!-- СВЕЖИЕ НОВОСТИ (только одна новость) -->
            <div class="section-content" id="section-news">
                <h2>📰 Свежие новости</h2>
                <div class="news-item">
                    <strong>9.07.26.</strong> Азар.А.Р. выкупил территорию у государства. Подробнее можно узнать у правителя или в разделе <strong>«Информация для правительства»</strong>.
                </div>
            </div>

            <!-- ИМУЩЕСТВО -->
            <div class="section-content" id="section-property">
                <h2>🏛️ Имущество</h2>
                <p class="empty-message">Здесь пока ничего нет.</p>
                <ul>
                    <li>—</li>
                </ul>
            </div>

            <!-- ИНФОРМАЦИЯ ДЛЯ ПРАВИТЕЛЬСТВА (с паролем) -->
            <div class="section-content" id="section-government">
                <h2>🏛️ Информация для правительства</h2>
                <p><strong>Секретные сведения</strong></p>
                <p class="empty-message">Здесь пока ничего нет. Требуется авторизация.</p>
                <ul style="list-style: none; padding-left: 0; margin-top: 12px;">
                    <li style="padding: 0.5rem 0 0.5rem 2.2rem; border-bottom: 1px dotted #4d3a2b; position: relative;">
                        <span style="position: absolute; left: 0; color: #d4af37;">⚜️</span> Доступ только по паролю
                    </li>
                </ul>
            </div>

        </div>

        <div class="ornament">⚜️ ⚜️ ⚜️</div>
    </div>

    <!-- Модальное окно для пароля -->
    <div class="password-overlay" id="passwordOverlay">
        <div class="password-modal">
            <h3>🔒 Доступ ограничен</h3>
            <p>Введите пароль для доступа к разделу<br><strong style="color: #d4af37;">«Информация для правительства»</strong></p>
            <input type="password" id="passwordInput" placeholder="Введите пароль" autofocus>
            <div class="password-error" id="passwordError">❌ Неверный пароль. Попробуйте снова.</div>
            <div class="btn-group">
                <button class="cancel" id="passwordCancel">Отмена</button>
                <button id="passwordSubmit">Войти</button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const buttons = document.querySelectorAll('.nav-btn');
            const sections = {
                rules: document.getElementById('section-rules'),
                news: document.getElementById('section-news'),
                property: document.getElementById('section-property'),
                government: document.getElementById('section-government')
            };

            const governmentBtn = document.getElementById('governmentBtn');
            const passwordOverlay = document.getElementById('passwordOverlay');
            const passwordInput = document.getElementById('passwordInput');
            const passwordError = document.getElementById('passwordError');
            const passwordSubmit = document.getElementById('passwordSubmit');
            const passwordCancel = document.getElementById('passwordCancel');

            const CORRECT_PASSWORD = '989357';

            buttons.forEach(btn => {
                btn.addEventListener('click', function() {
                    if (this.id === 'governmentBtn') {
                        passwordOverlay.classList.add('show');
                        passwordInput.value = '';
                        passwordError.classList.remove('show');
                        setTimeout(() => passwordInput.focus(), 100);
                        return;
                    }
                    switchSection(this.getAttribute('data-section'));
                });
            });

            function switchSection(sectionId) {
                buttons.forEach(b => b.classList.remove('active'));
                buttons.forEach(b => {
                    if (b.getAttribute('data-section') === sectionId) {
                        b.classList.add('active');
                    }
                });
                Object.values(sections).forEach(section => {
                    section.classList.remove('active');
                });
                if (sections[sectionId]) {
                    sections[sectionId].classList.add('active');
                }
            }

            function checkPassword() {
                const entered = passwordInput.value.trim();
                if (entered === CORRECT_PASSWORD) {
                    passwordOverlay.classList.remove('show');
                    passwordError.classList.remove('show');
                    switchSection('government');
                    buttons.forEach(b => b.classList.remove('active'));
                    governmentBtn.classList.add('active');
                } else {
                    passwordError.classList.add('show');
                    passwordInput.value = '';
                    passwordInput.focus();
                }
            }

            passwordSubmit.addEventListener('click', checkPassword);

            passwordInput.addEventListener('keydown', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    checkPassword();
                }
                if (e.key === 'Escape') {
                    passwordOverlay.classList.remove('show');
                    passwordError.classList.remove('show');
                }
            });

            passwordCancel.addEventListener('click', function() {
                passwordOverlay.classList.remove('show');
                passwordError.classList.remove('show');
            });

            passwordOverlay.addEventListener('click', function(e) {
                if (e.target === this) {
                    passwordOverlay.classList.remove('show');
                    passwordError.classList.remove('show');
                }
            });
        });
    </script>
</body>
</html>

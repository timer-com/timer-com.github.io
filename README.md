<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Республика «Team» / Советская империя</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            min-height:100vh;
            background:#0b0d11;
            display:flex;
            justify-content:center;
            align-items:center;
            padding:20px;
        }
        .switch-container {
            position:fixed; top:20px; right:20px; z-index:9999;
            display:flex; gap:10px; flex-wrap:wrap; justify-content:flex-end;
        }
        .switch-btn {
            padding:0.6rem 1.4rem; border-radius:40px; border:2px solid #d4af37;
            background:rgba(0,0,0,0.7); backdrop-filter:blur(8px);
            color:#f5e7d3; font-size:0.9rem; font-weight:600; cursor:pointer;
            transition:0.3s; font-family:'Segoe UI',sans-serif;
            box-shadow:0 4px 20px rgba(0,0,0,0.5);
        }
        .switch-btn:hover { background:#d4af37; color:#1a1a1a; transform:scale(1.05); }
        .switch-btn.active { background:#d4af37; color:#1a1a1a; border-color:#f5e7d3; }

        .site-container {
            display:none; width:100%; max-width:1300px;
            animation:fadeIn 0.4s ease;
        }
        .site-container.active { display:block; }
        @keyframes fadeIn { from { opacity:0; transform:scale(0.97); } to { opacity:1; transform:scale(1); } }

        /* ===== СТИЛИ ДЛЯ САЙТА РЕСПУБЛИКИ TEAM ===== */
        .team-wrapper {
            background: radial-gradient(circle at 20% 30%, #141a24, #07090e 80%);
            min-height: 100vh; border-radius: 2rem; padding: 2rem 2rem 1rem;
            box-shadow: 0 0 40px rgba(0, 20, 40, 0.6);
        }
        .team-header {
            display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;
            padding-bottom: 1.5rem; border-bottom: 1px solid #2a354a; margin-bottom: 2.5rem;
        }
        .team-logo { display: flex; align-items: center; gap: 0.75rem; }
        .team-logo i { font-size: 2.4rem; color: #64f0b0; filter: drop-shadow(0 0 6px #3ad68a); }
        .team-logo span { font-weight: 700; font-size: 2rem; background: linear-gradient(135deg, #c0e6ff, #6ec8ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .team-logo span small { font-weight: 300; color: #b0c9e8; -webkit-text-fill-color: #b0c9e8; background: none; }
        .team-nav { display: flex; gap: 1.8rem; align-items: center; flex-wrap: wrap; }
        .team-nav a { color: #b6cae5; text-decoration: none; font-weight: 500; font-size: 1.1rem; cursor: pointer; border-bottom: 2px solid transparent; padding-bottom: 4px; transition: 0.2s; }
        .team-nav a:hover { color: #b3f0d0; border-bottom-color: #52d79a; }
        .team-content { color: #eef2f6; }
        .team-content h2 { font-size: 2.2rem; margin: 2rem 0 1.5rem; display: flex; align-items: center; gap: 12px; color: #d4ebff; }
        .team-content h2 i { color: #55dba0; }
        .team-content p { color: #b6cae5; line-height: 1.8; font-size: 1.05rem; }
        .team-departments {
            display: flex; flex-wrap: wrap; gap: 1.5rem 2.5rem;
            background: rgba(12, 24, 38, 0.5); backdrop-filter: blur(4px);
            padding: 1.2rem 2rem; border-radius: 60px; border: 1px solid #2a4058;
            margin-bottom: 2.5rem; justify-content: center;
        }
        .team-dept { display: flex; align-items: center; gap: 10px; color: #c6defa; font-size: 1.1rem; font-weight: 500; }
        .team-dept i { color: #59dba6; font-size: 1.3rem; width: 1.6rem; text-align: center; }
        .team-dept .divider { color: #3a5a6a; margin-left: 0.2rem; }
        .team-codex {
            background: #0d1a26; border-radius: 40px; padding: 2rem 2.5rem;
            margin: 2rem 0; border-left: 6px solid #f0c060;
            box-shadow: 0 0 20px rgba(240, 192, 96, 0.08);
        }
        .team-codex h3 { font-size: 1.8rem; color: #f5e3c0; display: flex; align-items: center; gap: 12px; margin-bottom: 1.2rem; }
        .team-codex h3 i { color: #f0c060; }
        .team-article { margin-bottom: 1.5rem; padding-left: 0.5rem; }
        .team-article .art-title { font-size: 1.2rem; font-weight: 600; color: #f0dba0; display: flex; align-items: center; gap: 8px; }
        .team-article .art-title i { color: #f0b84d; }
        .team-article .art-text { color: #d0def0; padding-left: 1.8rem; margin-bottom: 0.5rem; border-left: 2px solid #3a5f6b; }
        .team-article .art-sub { padding-left: 2.5rem; color: #b9ceea; font-size: 0.98rem; }
        .team-article .art-sub i { color: #f0b84d; width: 1.4rem; }

        /* ===== СТИЛИ ДЛЯ САЙТА СОВЕТСКОЙ ИМПЕРИИ ===== */
        .empire-wrapper {
            background: rgba(0,0,0,0.85); backdrop-filter:blur(4px);
            border-radius:40px; padding:2rem 2.2rem;
            box-shadow:0 20px 40px rgba(0,0,0,0.7),0 0 0 2px #FFD700,0 0 0 4px #1a1a1a;
            border:1px solid #d4af37;
        }
        .empire-header {
            display:flex; align-items:center; gap:24px; flex-wrap:wrap;
            border-bottom:2px solid #d4af37; padding-bottom:1.2rem; margin-bottom:1.8rem;
        }
        .empire-flag {
            flex-shrink:0; width:130px; height:75px; border-radius:10px; overflow:hidden;
            border:2px solid #d4af37; box-shadow:0 4px 12px rgba(0,0,0,0.6);
            display:flex; flex-direction:column;
        }
        .empire-flag .stripe { flex:1; width:100%; }
        .empire-flag .black { background:#000; }
        .empire-flag .yellow { background:#FFD700; }
        .empire-flag .white { background:#FFF; }
        .empire-title {
            font-size:2.6rem; font-weight:700; letter-spacing:4px;
            color:#f5e7d3; text-shadow:0 4px 14px #000000cc,0 0 10px #d4af37aa;
            font-family:'Times New Roman',serif; flex:1;
        }
        .empire-title small { font-size:1rem; font-weight:300; letter-spacing:6px; display:block; color:#e6d5b8; }
        .empire-login {
            display:flex; gap:10px; align-items:center; flex-shrink:0;
        }
        .empire-login .user-info { color:#f5e7d3; font-size:0.9rem; }
        .empire-login .user-info strong { color:#d4af37; }
        .empire-login button {
            background:rgba(30,25,20,0.7); border:1px solid #d4af37; border-radius:60px;
            padding:0.4rem 1.2rem; color:#f5e7d3; cursor:pointer; transition:0.2s;
            font-size:0.85rem; font-family:'Segoe UI',sans-serif;
        }
        .empire-login button:hover { background:#d4af37; color:#1a1a1a; }
        .empire-nav {
            display:flex; flex-wrap:wrap; gap:12px; margin-bottom:1.5rem;
            justify-content:center;
        }
        .empire-nav .nav-btn {
            flex:1 0 auto; min-width:120px; padding:0.8rem 1.6rem;
            background:rgba(30,25,20,0.7); backdrop-filter:blur(2px);
            border:1px solid #d4af37; border-radius:60px;
            color:#f5e7d3; font-size:1.1rem; font-weight:500; letter-spacing:1.5px;
            text-align:center; cursor:pointer; transition:0.2s;
            box-shadow:0 4px 12px rgba(0,0,0,0.3);
            font-family:'Segoe UI',sans-serif; user-select:none;
        }
        .empire-nav .nav-btn:hover { background:rgba(60,45,35,0.8); border-color:#e6c14f; transform:scale(1.02); }
        .empire-nav .nav-btn.active { background:#d4af37; color:#1a1a1a; border-color:#f5e7d3; box-shadow:0 0 30px #d4af3766; }
        .empire-content {
            background:rgba(30,25,20,0.5); border-radius:28px;
            border:1px solid #d4af37; padding:2rem; overflow-y:auto; max-height:55vh;
        }
        .empire-content::-webkit-scrollbar { width:8px; }
        .empire-content::-webkit-scrollbar-track { background:rgba(30,25,20,0.3); border-radius:10px; }
        .empire-content::-webkit-scrollbar-thumb { background:#d4af37; border-radius:10px; }
        .empire-section { display:none; height:100%; color:#f0e6da; }
        .empire-section.active { display:block; }
        .empire-section h2 {
            font-family:'Times New Roman',serif; font-weight:700; font-size:2rem;
            color:#f5e2c9; border-bottom:2px solid #d4af37; padding-bottom:0.8rem;
            margin-bottom:1.5rem; letter-spacing:2px; text-shadow:0 2px 6px #000000aa;
        }
        .empire-section h3 { font-family:'Times New Roman',serif; font-size:1.3rem; color:#f5d742; margin:1.2rem 0 0.8rem; }
        .empire-section p { font-size:1.05rem; line-height:1.8; color:#e2d4c2; margin-bottom:0.8rem; }
        .empire-section ul { list-style:none; padding-left:0; }
        .empire-section ul li { padding:0.4rem 0 0.4rem 2.2rem; position:relative; border-bottom:1px dotted #4d3a2b; }
        .empire-section ul li::before { content:"⚜️"; position:absolute; left:0; color:#d4af37; }
        .empire-rule { background:rgba(0,0,0,0.25); border-left:3px solid #d4af37; padding:0.8rem 1.2rem; border-radius:8px; margin-bottom:0.8rem; }
        .empire-rule .rule-num { color:#f5d742; font-weight:600; }
        .empire-news { background:rgba(0,0,0,0.3); border-left:4px solid #d4af37; padding:1rem 1.2rem; border-radius:12px; margin-bottom:1rem; }
        .empire-news strong { color:#f5d742; font-weight:600; }
        .empire-ornament { text-align:center; color:#d4af37; letter-spacing:6px; font-size:0.8rem; margin-top:1rem; opacity:0.7; }
        .empire-demo { color:#8a7a6a; font-size:0.8rem; text-align:center; margin-top:0.5rem; border-top:1px solid #4d3a2b; padding-top:0.5rem; }

        /* ===== МОДАЛЬНОЕ ОКНО ВХОДА ===== */
        .empire-modal {
            display:none; position:fixed; top:0; left:0; width:100%; height:100%;
            background:rgba(0,0,0,0.85); backdrop-filter:blur(8px);
            z-index:10000; justify-content:center; align-items:center;
        }
        .empire-modal.active { display:flex; }
        .empire-modal .modal-box {
            background:#1a1a1a; border-radius:32px; padding:2.5rem;
            max-width:400px; width:90%;
            border:2px solid #d4af37; box-shadow:0 0 60px rgba(212,175,55,0.2);
        }
        .empire-modal .modal-box h2 {
            color:#f5e7d3; font-family:'Times New Roman',serif; font-size:1.8rem;
            margin-bottom:0.3rem; text-align:center;
        }
        .empire-modal .modal-box .sub {
            color:#8a7a6a; text-align:center; margin-bottom:1.5rem; font-size:0.9rem;
        }
        .empire-modal .modal-box label {
            display:block; color:#b6a68a; margin-bottom:0.3rem; font-weight:500;
        }
        .empire-modal .modal-box input {
            width:100%; padding:0.8rem 1rem; border-radius:16px;
            border:1px solid #4d3a2b; background:#0a0a0a; color:#f5e7d3;
            font-size:1rem; margin-bottom:1.2rem; outline:none;
        }
        .empire-modal .modal-box input:focus { border-color:#d4af37; box-shadow:0 0 12px #d4af3744; }
        .empire-modal .modal-box .btn-go {
            width:100%; padding:0.9rem; border:none; border-radius:40px;
            background:linear-gradient(145deg, #d4af37, #b8962a);
            color:#1a1a1a; font-weight:700; font-size:1.1rem; cursor:pointer;
            transition:0.2s; box-shadow:0 0 20px #d4af3744;
        }
        .empire-modal .modal-box .btn-go:hover { transform:scale(1.02); box-shadow:0 0 32px #d4af3766; }
        .empire-modal .modal-box .error {
            color:#ff6b4a; font-size:0.9rem; margin:-0.3rem 0 0.8rem 0; display:none;
        }
        .empire-modal .modal-box .error.show { display:block; }
        .empire-modal .modal-box .close-modal {
            float:right; font-size:1.8rem; color:#8a7a6a; cursor:pointer;
            background:none; border:none; transition:0.2s;
        }
        .empire-modal .modal-box .close-modal:hover { color:#ff6b4a; transform:rotate(90deg); }

        /* ===== ТОСТ ===== */
        .toast {
            position:fixed; bottom:2rem; left:50%; transform:translateX(-50%);
            background:#1a2a34; padding:0.8rem 2rem; border-radius:60px;
            border:1px solid #3a5a6a; box-shadow:0 0 30px rgba(0,0,0,0.6);
            z-index:99999; display:none; font-size:1rem;
            backdrop-filter:blur(8px); text-align:center; max-width:90%;
            color:#f5e7d3;
        }
        .toast.show { display:block; animation:fadeInUp 0.3s ease; }
        .toast.success { border-color:#56dba7; }
        .toast.error { border-color:#ff5a5a; }
        .toast i { margin-right:8px; }
        @keyframes fadeInUp { from { opacity:0; transform:translateX(-50%) translateY(20px); } to { opacity:1; transform:translateX(-50%) translateY(0); } }

        @media (max-width:900px) {
            .empire-title { font-size:2rem; }
            .empire-flag { width:100px; height:58px; }
            .empire-nav .nav-btn { white-space:normal; min-width:80px; padding:0.6rem 1rem; font-size:0.95rem; }
            .empire-content { padding:1.2rem; }
            .team-wrapper { padding:1rem; }
            .empire-login { margin-left:0; }
        }
        @media (max-width:550px) {
            .empire-header { flex-direction:column; align-items:flex-start; gap:12px; }
            .empire-title { font-size:1.6rem; }
            .empire-title small { font-size:0.8rem; letter-spacing:3px; }
            .empire-nav .nav-btn { min-width:60px; font-size:0.85rem; padding:0.5rem 0.8rem; }
            .empire-content { padding:0.8rem; }
            .empire-section h2 { font-size:1.3rem; }
            .team-header { flex-direction:column; align-items:stretch; gap:1.2rem; }
            .team-nav { justify-content:center; }
            .empire-login { width:100%; justify-content:flex-start; }
        }
    </style>
</head>
<body>

    <div class="switch-container">
        <button class="switch-btn active" id="switchToTeam" onclick="switchSite('team')">🏛️ Республика Team</button>
        <button class="switch-btn" id="switchToEmpire" onclick="switchSite('empire')">👑 Советская империя</button>
    </div>

    <!-- ===== САЙТ РЕСПУБЛИКИ TEAM ===== -->
    <div class="site-container active" id="site-team">
        <div class="team-wrapper">
            <header class="team-header">
                <div class="team-logo">
                    <i class="fas fa-flag"></i>
                    <span>Республика <small>Team</small></span>
                </div>
                <nav class="team-nav">
                    <a href="#"><i class="fas fa-users"></i> Отделы</a>
                    <a href="#"><i class="fas fa-store"></i> Магазин</a>
                    <a href="#"><i class="fas fa-book"></i> Библиотека</a>
                    <a href="#"><i class="fas fa-coins"></i> Финансы</a>
                    <a href="#"><i class="fas fa-id-card"></i> Паспорт</a>
                </nav>
            </header>

            <div class="team-content">
                <div class="team-departments">
                    <span class="team-dept"><i class="fas fa-gavel"></i> Юридический <span class="divider">|</span></span>
                    <span class="team-dept"><i class="fas fa-hand-holding-heart"></i> Социальный <span class="divider">|</span></span>
                    <span class="team-dept"><i class="fas fa-chart-line"></i> Экономики</span>
                </div>

                <h2><i class="fas fa-sitemap"></i> Отделы республики</h2>
                <p>Юридический отдел — нормотворчество, арбитраж, защита прав граждан.<br>
                Социальный отдел — поддержка граждан, волонтёрство, внутренние коммуникации.<br>
                Отдел экономики — финансы, бюджетирование, налоги, гранты, инвестиции.</p>

                <div class="team-codex">
                    <h3><i class="fas fa-scroll"></i> Кодекс правил Республики «Team»</h3>
                    <div class="team-article">
                        <div class="art-title"><i class="fas fa-balance-scale"></i> 1. Выкуп имущества</div>
                        <div class="art-text">При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если покупатель решил отменить сделку, он должен выплатить государству компенсацию 6 000 рублей.</div>
                        <div class="art-sub"><i class="fas fa-chevron-right"></i> 1.1. Отменить договор можно при согласии всех членов правительства в течение 1 дня (мелкая сделка) или 2 дней (крупная).</div>
                        <div class="art-sub"><i class="fas fa-chevron-right"></i> 1.2. Если налоговой службе не понравится происхождение денег, государство может отменить сделку и не выплачивать компенсацию.</div>
                    </div>
                    <div class="team-article">
                        <div class="art-title"><i class="fas fa-car-crash"></i> 2. Нарушения на дороге</div>
                        <div class="art-text">Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</div>
                        <div class="art-sub"><i class="fas fa-minus"></i> В первый раз — штраф 10 рублей</div>
                        <div class="art-sub"><i class="fas fa-minus"></i> Во второй и следующие разы — штраф и лишение свободы на 1 день</div>
                    </div>
                    <div class="team-article">
                        <div class="art-title"><i class="fas fa-truck"></i> 3. При ДТП на дороге</div>
                        <div class="art-sub"><i class="fas fa-check-circle"></i> Штраф платит виноватый — 5 000 рублей</div>
                        <div class="art-sub"><i class="fas fa-check-circle"></i> Пострадавший получает компенсацию 6 000 рублей</div>
                        <div class="art-sub"><i class="fas fa-check-circle"></i> Государству выплаты не производятся</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- ===== САЙТ СОВЕТСКОЙ ИМПЕРИИ ===== -->
    <div class="site-container" id="site-empire">
        <div class="empire-wrapper">
            <header class="empire-header">
                <div class="empire-flag">
                    <div class="stripe black"></div>
                    <div class="stripe yellow"></div>
                    <div class="stripe white"></div>
                </div>
                <div class="empire-title">
                    Сайт Советской империи
                    <small>⚜️ Самодержавие · Православие · Народность ⚜️</small>
                </div>
                <div class="empire-login">
                    <span class="user-info" id="empireUserInfo">Гость</span>
                    <button id="empireLoginBtn" onclick="openEmpireLogin()">Войти</button>
                </div>
            </header>

            <div class="empire-nav">
                <button class="nav-btn active" data-section="rules">📜 Правила</button>
                <button class="nav-btn" data-section="news">📰 Новости</button>
                <button class="nav-btn" data-section="property">🏛️ Имущество</button>
                <button class="nav-btn" data-section="gov">🏛️ Инфо для правительства</button>
            </div>

            <div class="empire-content">
                <!-- ПРАВИЛА -->
                <div class="empire-section active" id="section-rules">
                    <h2>📜 Кодекс правил Советской Империи</h2>
                    <h3>1. Выкуп имущества</h3>
                    <div class="empire-rule"><p><span class="rule-num">1.</span> При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если же договор был составлен и подписан и покупатель решил отменить сделку, то он должен выплатить государству компенсацию в размере <strong>6 000 рублей</strong>, в случае отмены сделки государством, государство не должно выплачивать компенсацию (подробнее в статье 1.2).</p></div>
                    <div class="empire-rule"><p><span class="rule-num">1.1.</span> Отменить договор можно при согласии всех членов правительства в течение <strong>1 дня</strong> на мелкую сделку и <strong>2 дней</strong> на крупную сделку.</p></div>
                    <div class="empire-rule"><p><span class="rule-num">1.2.</span> Если налоговой службе не понравится происхождение денег, выплаченных покупателем, то государство может отменить сделку (подробнее в статье 1.1.) и <strong>не выплачивать компенсацию</strong> покупателю. Государство может забрать эти деньги и вообще не отдавать их покупателю.</p></div>
                    <h3>2. Нарушения на дороге</h3>
                    <div class="empire-rule"><p><span class="rule-num">2.</span> Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</p><ul><li><strong>В первый раз</strong> — обязан выплатить штраф <strong>10 рублей</strong></li><li><strong>Во второй и следующие разы</strong> — выплачивает штраф и лишается свободы на срок <strong>1 день</strong></li></ul><p style="margin-top:0.5rem;font-style:italic;color:#c7b7a2;">*При лишении свободы деятельность человека прекращается на указанный срок.</p></div>
                    <div class="empire-rule"><p><span class="rule-num">3.</span> При ДТП на дороге:</p><ul><li><strong>Вина</strong> — штраф оплачивает только <strong>виноватый</strong> участник</li><li><strong>Штраф виноватому</strong> — <strong>5 000 рублей</strong></li><li><strong>Пострадавшему</strong> — выплачивается компенсация <strong>6 000 рублей</strong></li><li><strong>Государству</strong> — выплаты не производятся</li></ul><p style="margin-top:0.5rem;font-style:italic;color:#c7b7a2;">*Без суда и решения штраф не выплачивается.</p></div>
                </div>

                <!-- НОВОСТИ -->
                <div class="empire-section" id="section-news">
                    <h2>📰 Свежие новости</h2>
                    <div class="empire-news"><strong>9.07.26.</strong> Азар.А.Р. выкупил территорию у государства. Подробнее можно узнать у правителя или в разделе <strong>«Информация для правительства»</strong>.</div>
                </div>

                <!-- ИМУЩЕСТВО -->
                <div class="empire-section" id="section-property">
                    <h2>🏛️ Имущество</h2>
                    <p style="opacity:0.7;font-style:italic;color:#c7b7a2;">Здесь пока ничего нет.</p>
                </div>

                <!-- ИНФО ДЛЯ ПРАВИТЕЛЬСТВА -->
                <div class="empire-section" id="section-gov">
                    <h2>🏛️ Информация для правительства</h2>
                    <p><strong>Секретные сведения</strong></p>
                    <p style="opacity:0.7;font-style:italic;color:#c7b7a2;">Здесь пока ничего нет. Требуется авторизация.</p>
                    <ul style="list-style:none;padding-left:0;margin-top:12px;">
                        <li style="padding:0.5rem 0 0.5rem 2.2rem;border-bottom:1px dotted #4d3a2b;position:relative;">
                            <span style="position:absolute;left:0;color:#d4af37;">⚜️</span> Доступ только по паролю
                        </li>
                    </ul>
                </div>
            </div>
            <div class="empire-ornament">⚜️ ⚜️ ⚜️</div>
            <div class="empire-demo">🔧 Демо-версия. Для работы регистрации и админки нужен сервер.</div>
        </div>
    </div>

    <!-- ===== МОДАЛЬНОЕ ОКНО ВХОДА ДЛЯ ИМПЕРИИ ===== -->
    <div class="empire-modal" id="empireLoginModal">
        <div class="modal-box">
            <button class="close-modal" onclick="closeEmpireLogin()">&times;</button>
            <h2><i class="fas fa-crown" style="color:#d4af37;"></i> Вход в империю</h2>
            <p class="sub">Введите логин и пароль</p>
            <label>Логин</label>
            <input type="text" id="empireLoginUser" placeholder="Андрей, Ярослав или Богдан">
            <label>Пароль</label>
            <input type="password" id="empireLoginPass" placeholder="Введите пароль">
            <div class="error" id="empireLoginError">Неверный логин или пароль</div>
            <button class="btn-go" onclick="empireDoLogin()"><i class="fas fa-sign-in-alt"></i> Войти</button>
        </div>
    </div>

    <!-- ===== ТОСТ ===== -->
    <div class="toast" id="toast"><i class="fas fa-check-circle"></i> <span id="toastMsg">Успешно!</span></div>

    <script>
        // ===== ДАННЫЕ АККАУНТОВ ДЛЯ СОВЕТСКОЙ ИМПЕРИИ =====
        var empireUsers = {
            'Андрей': '567384',
            'Ярослав': '274890',
            'Богдан': '309940'
        };

        var empireCurrentUser = null;

        // ===== ТОСТ =====
        function showToast(msg, type) {
            var toast = document.getElementById('toast');
            var toastMsg = document.getElementById('toastMsg');
            toastMsg.textContent = msg;
            toast.className = 'toast show ' + type;
            clearTimeout(toast._timer);
            toast._timer = setTimeout(function() { toast.classList.remove('show'); }, 3500);
        }

        // ===== ПЕРЕКЛЮЧЕНИЕ МЕЖДУ САЙТАМИ =====
        function switchSite(site) {
            document.querySelectorAll('.site-container').forEach(el => el.classList.remove('active'));
            document.getElementById('site-' + site).classList.add('active');
            document.querySelectorAll('.switch-btn').forEach(btn => btn.classList.remove('active'));
            if (site === 'team') {
                document.getElementById('switchToTeam').classList.add('active');
            } else {
                document.getElementById('switchToEmpire').classList.add('active');
            }
        }

        // ===== НАВИГАЦИЯ НА САЙТЕ ИМПЕРИИ =====
        document.querySelectorAll('.empire-nav .nav-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.empire-nav .nav-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                document.querySelectorAll('.empire-section').forEach(el => el.classList.remove('active'));
                document.getElementById('section-' + this.dataset.section).classList.add('active');
            });
        });

        // ===== АВТОРИЗАЦИЯ ДЛЯ ИМПЕРИИ =====
        function openEmpireLogin() {
            if (empireCurrentUser) return;
            document.getElementById('empireLoginModal').classList.add('active');
            document.getElementById('empireLoginError').classList.remove('show');
            document.getElementById('empireLoginUser').value = '';
            document.getElementById('empireLoginPass').value = '';
            setTimeout(function() { document.getElementById('empireLoginUser').focus(); }, 100);
        }

        function closeEmpireLogin() {
            document.getElementById('empireLoginModal').classList.remove('active');
        }

        function empireDoLogin() {
            var login = document.getElementById('empireLoginUser').value.trim();
            var pass = document.getElementById('empireLoginPass').value.trim();

            if (empireUsers[login] && empireUsers[login] === pass) {
                empireCurrentUser = login;
                document.getElementById('empireLoginModal').classList.remove('active');
                updateEmpireUI();
                showToast('Добро пожаловать, ' + login + '!', 'success');
            } else {
                document.getElementById('empireLoginError').classList.add('show');
            }
        }

        function empireLogout() {
            empireCurrentUser = null;
            updateEmpireUI();
            showToast('Вы вышли из аккаунта', 'error');
        }

        function updateEmpireUI() {
            var userInfo = document.getElementById('empireUserInfo');
            var loginBtn = document.getElementById('empireLoginBtn');

            if (empireCurrentUser) {
                userInfo.innerHTML = '<i class="fas fa-user-circle" style="color:#d4af37;"></i> <strong>' + empireCurrentUser + '</strong>';
                loginBtn.textContent = 'Выйти';
                loginBtn.onclick = empireLogout;
            } else {
                userInfo.textContent = 'Гость';
                loginBtn.textContent = 'Войти';
                loginBtn.onclick = openEmpireLogin;
            }
        }

        // Закрытие модалки по клику вне
        document.getElementById('empireLoginModal').addEventListener('click', function(e) {
            if (e.target === this) closeEmpireLogin();
        });

        // Enter на полях входа
        document.getElementById('empireLoginUser').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') { e.preventDefault(); empireDoLogin(); }
        });
        document.getElementById('empireLoginPass').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') { e.preventDefault(); empireDoLogin(); }
        });

        // ===== ИНИЦИАЛИЗАЦИЯ =====
        document.addEventListener('DOMContentLoaded', function() {
            updateEmpireUI();
        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Республика «Team»</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Roboto, sans-serif; }
        body { background: #0b0d11; color: #eef2f6; }
        .site-wrapper {
            max-width: 1300px; margin: 0 auto; padding: 2rem 2rem 1rem;
            background: radial-gradient(circle at 20% 30%, #141a24, #07090e 80%);
            min-height: 100vh; border-radius: 2rem 2rem 0 0;
        }
        .header {
            display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;
            padding-bottom: 1.5rem; border-bottom: 1px solid #2a354a; margin-bottom: 2.5rem;
        }
        .logo-block { display: flex; align-items: center; gap: 0.75rem; }
        .logo-icon { font-size: 2.4rem; color: #64f0b0; filter: drop-shadow(0 0 6px #3ad68a); }
        .logo-text { font-weight: 700; font-size: 2rem; background: linear-gradient(135deg, #c0e6ff, #6ec8ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .logo-text span { font-weight: 300; color: #b0c9e8; -webkit-text-fill-color: #b0c9e8; background: none; }
        .nav { display: flex; gap: 1.8rem; align-items: center; flex-wrap: wrap; }
        .nav a { color: #b6cae5; text-decoration: none; font-weight: 500; font-size: 1.1rem; cursor: pointer; border-bottom: 2px solid transparent; padding-bottom: 4px; transition: 0.2s; }
        .nav a:hover { color: #b3f0d0; border-bottom-color: #52d79a; }
        .btn-login {
            padding: 0.5rem 1.4rem; border-radius: 40px; font-size: 1rem; font-weight: 500;
            cursor: pointer; display: inline-flex; align-items: center; gap: 8px; border: none;
            background: linear-gradient(145deg, #2cdf8a, #1db06e); color: #0b141c;
            box-shadow: 0 0 20px #24d17e44; transition: 0.2s;
        }
        .btn-login:hover { transform: scale(1.02); box-shadow: 0 0 32px #2bff9a66; }
        .section-title { font-size: 2.2rem; margin: 3rem 0 1.8rem; display: flex; align-items: center; gap: 12px; }
        .section-title i { color: #55dba0; font-size: 2rem; }
        .departments-strip {
            display: flex; flex-wrap: wrap; gap: 1.5rem 2.5rem;
            background: rgba(12, 24, 38, 0.5); backdrop-filter: blur(4px);
            padding: 1.2rem 2rem; border-radius: 60px; border: 1px solid #2a4058;
            margin-bottom: 2.5rem; justify-content: center;
        }
        .dept-tag { display: flex; align-items: center; gap: 10px; color: #c6defa; font-size: 1.1rem; font-weight: 500; }
        .dept-tag i { color: #59dba6; font-size: 1.3rem; width: 1.6rem; text-align: center; }
        .dept-tag .divider { color: #3a5a6a; margin-left: 0.2rem; }
        .codex-block {
            background: #0d1a26; border-radius: 40px; padding: 2rem 2.5rem;
            margin: 2.5rem 0; border-left: 6px solid #f0c060;
            box-shadow: 0 0 20px rgba(240, 192, 96, 0.08);
            scroll-margin-top: 80px;
        }
        .codex-block h2 { font-size: 2rem; color: #f5e3c0; display: flex; align-items: center; gap: 12px; margin-bottom: 1.5rem; }
        .codex-block h2 i { color: #f0c060; }
        .codex-article { margin-bottom: 2rem; padding-left: 0.5rem; }
        .codex-article .article-title { font-size: 1.3rem; font-weight: 600; color: #f0dba0; display: flex; align-items: center; gap: 8px; }
        .codex-article .article-title i { color: #f0b84d; }
        .codex-article .article-text { color: #d0def0; padding-left: 1.8rem; margin-bottom: 0.8rem; border-left: 2px solid #3a5f6b; }
        .codex-sub { padding-left: 2.5rem; color: #b9ceea; margin-top: 0.2rem; font-size: 0.98rem; }
        .codex-sub i { color: #f0b84d; width: 1.4rem; }
        .passport-box {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 1.8rem; border: 1px solid #2d4560;
            max-width: 480px; margin: 2rem 0 1rem;
            scroll-margin-top: 80px;
        }
        .passport-box h3 { font-size: 1.6rem; margin-bottom: 1rem; color: #d4ebff; display: flex; align-items: center; gap: 10px; }
        .passport-box h3 i { color: #4edb9e; }
        .passport-box ul { list-style: none; }
        .passport-box ul li { padding: 0.5rem 0; border-bottom: 1px solid #1f344a; color: #bdd6f0; display: flex; align-items: center; gap: 10px; }
        .passport-box ul li i { color: #51d49b; width: 1.4rem; }
        .passport-id { background: #0a1a28; border-radius: 20px; padding: 0.8rem 1.2rem; margin-top: 1rem; border: 1px solid #2f6880; display: flex; align-items: center; gap: 1rem; }
        .passport-id i { font-size: 2rem; color: #6ad4a8; }
        .passport-id .id-number { font-family: 'Courier New', monospace; letter-spacing: 2px; font-size: 1.2rem; color: #b3f0d0; }

        /* ===== ФИНАНСЫ ===== */
        .finance-block {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 2.5rem;
            border: 1px solid #2d4560;
            max-width: 500px; margin: 2rem 0 1rem;
            scroll-margin-top: 80px;
            border-left: 6px solid #f0c060;
        }
        .finance-block h3 { font-size: 1.6rem; margin-bottom: 0.5rem; color: #d4ebff; display: flex; align-items: center; gap: 10px; }
        .finance-block h3 i { color: #f0b84d; }
        .finance-block .balance {
            font-size: 2.8rem; font-weight: 700;
            background: linear-gradient(135deg, #f5e3c0, #f0c060);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            margin: 0.5rem 0 0.3rem;
        }
        .finance-block .currency { font-size: 1.2rem; color: #b0c9e8; -webkit-text-fill-color: #b0c9e8; }
        .finance-block .label { color: #8eb3d4; font-size: 0.9rem; }

        .footer { margin-top: 4rem; padding: 2rem 0 1rem; border-top: 1px solid #23344a; display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; gap: 1.5rem; }
        .footer-social a { color: #96b8dd; font-size: 1.5rem; margin: 0 0.6rem; transition: 0.2s; }
        .footer-social a:hover { color: #60e6aa; transform: scale(1.1); }
        .footer-copy { color: #6c89aa; font-size: 0.95rem; }
        .footer-copy i { color: #48c78a; }
        .user-greeting { display: none; color: #b3f0d0; font-weight: 500; font-size: 1rem; align-items: center; gap: 8px; }
        .user-greeting i { color: #64f0b0; }
        .user-greeting .logout-btn { color: #ff8a8a; cursor: pointer; font-size: 0.9rem; border: 1px solid #ff5a5a44; padding: 0.2rem 0.8rem; border-radius: 20px; background: transparent; }
        .user-greeting .logout-btn:hover { background: #ff2a2a22; border-color: #ff5a5a; }

        #loginForm {
            display: none;
            background: rgba(12, 24, 38, 0.95);
            border-radius: 32px;
            padding: 2rem 2.5rem;
            border: 1px solid #3a5a7a;
            max-width: 400px;
            margin: 0 auto 2rem;
            box-shadow: 0 0 60px rgba(0, 60, 120, 0.2);
        }
        #loginForm.active { display: block; }
        #loginForm label { display: block; color: #b6ceea; margin-bottom: 0.3rem; font-weight: 500; }
        #loginForm input {
            width: 100%; padding: 0.8rem 1rem; border-radius: 16px;
            border: 1px solid #2f4a66; background: #0b1a28; color: #eef2f6;
            font-size: 1rem; margin-bottom: 1rem; outline: none;
        }
        #loginForm input:focus { border-color: #56dba7; box-shadow: 0 0 12px #2fbb7e44; }
        #loginForm .btn-go {
            width: 100%; padding: 0.9rem; border: none; border-radius: 40px;
            background: linear-gradient(145deg, #2cdf8a, #1db06e);
            color: #0b141c; font-weight: 700; font-size: 1.1rem; cursor: pointer;
            box-shadow: 0 0 20px #24d17e44; transition: 0.2s;
        }
        #loginForm .btn-go:hover { transform: scale(1.02); box-shadow: 0 0 32px #2bff9a66; }
        #loginForm .error { color: #ff7a7a; font-size: 0.9rem; margin: -0.3rem 0 0.8rem 0; display: none; }
        #loginForm .error.show { display: block; }
        #loginForm .close-form {
            float: right; font-size: 1.5rem; color: #88aacf; cursor: pointer;
            background: none; border: none; transition: 0.2s;
        }
        #loginForm .close-form:hover { color: #ff7a7a; transform: rotate(90deg); }

        .section-scroll { scroll-margin-top: 80px; }

        @media (max-width: 700px) {
            .header { flex-direction: column; align-items: stretch; gap: 1.2rem; }
            .nav { justify-content: center; }
            .site-wrapper { padding: 1rem; }
            .codex-block { padding: 1.5rem; }
            .codex-article .article-text { padding-left: 1rem; }
            .codex-sub { padding-left: 1.5rem; }
            .departments-strip { padding: 1rem; flex-direction: column; align-items: center; }
            .passport-box, .finance-block { max-width: 100%; }
            #loginForm { padding: 1.5rem; }
            .finance-block .balance { font-size: 2rem; }
        }
    </style>
</head>
<body>
<div class="site-wrapper">

    <header class="header">
        <div class="logo-block">
            <i class="fas fa-flag logo-icon"></i>
            <span class="logo-text">Республика <span>Team</span></span>
        </div>
        <nav class="nav">
            <a onclick="scrollToSection('departments')"><i class="fas fa-users"></i> Отделы</a>
            <a onclick="scrollToSection('codex')"><i class="fas fa-book"></i> Кодекс</a>
            <a onclick="scrollToSection('finance')"><i class="fas fa-coins"></i> Финансы</a>
            <a onclick="scrollToSection('passport')"><i class="fas fa-id-card"></i> Паспорт</a>
            <span class="user-greeting" id="greeting">
                <i class="fas fa-user-circle"></i>
                <span id="userName">Семён</span>
                <span class="logout-btn" onclick="logout()">Выйти</span>
            </span>
            <button class="btn-login" id="loginBtn" onclick="showLogin()">
                <i class="fas fa-sign-in-alt"></i> Войти
            </button>
        </nav>
    </header>

    <div id="loginForm">
        <button class="close-form" onclick="hideLogin()">&times;</button>
        <h2 style="color: #d4ebff; margin-bottom: 0.3rem;"><i class="fas fa-user-lock" style="color: #59dba6;"></i> Вход</h2>
        <p style="color: #8eb3d4; margin-bottom: 1.5rem;">Введите логин и пароль</p>
        <label>Логин</label>
        <input type="text" id="loginUser" placeholder="Семён, Азар или Вика">
        <label>Пароль</label>
        <input type="password" id="loginPass" placeholder="Введите пароль">
        <div class="error" id="loginError">Неверный логин или пароль</div>
        <button class="btn-go" onclick="doLogin()"><i class="fas fa-sign-in-alt"></i> Войти</button>
    </div>

    <h2 class="section-title section-scroll" id="departments"><i class="fas fa-sitemap"></i> Отделы республики</h2>
    <div class="departments-strip">
        <span class="dept-tag"><i class="fas fa-gavel"></i> Юридический <span class="divider">|</span></span>
        <span class="dept-tag"><i class="fas fa-hand-holding-heart"></i> Социальный <span class="divider">|</span></span>
        <span class="dept-tag"><i class="fas fa-chart-line"></i> Экономики</span>
    </div>

    <!-- ===== ФИНАНСЫ ===== -->
    <div class="finance-block section-scroll" id="finance">
        <h3><i class="fas fa-coins"></i> Финансы</h3>
        <div class="label">Банковский счёт</div>
        <div class="balance" id="balanceDisplay">0</div>
        <div class="currency">тимовских рублей</div>
        <div style="margin-top: 0.8rem; color: #8eb3d4; font-size: 0.9rem; border-top: 1px solid #1f344a; padding-top: 0.8rem;">
            <i class="fas fa-info-circle" style="color: #59dba6;"></i> 
            Владелец: <span id="financeOwner">Гость</span>
        </div>
    </div>

    <div class="codex-block section-scroll" id="codex">
        <h2><i class="fas fa-scroll"></i> Кодекс правил Республики «Team»</h2>
        <div class="codex-article">
            <div class="article-title"><i class="fas fa-balance-scale"></i> 1. Выкуп имущества</div>
            <div class="article-text">1. При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если же договор был составлен и подписан и покупатель решил отменить сделку, то он должен выплатить государству компенсацию в размере 6 000 рублей, в случае отмены сделки государством, государство не должно выплачивать компенсацию (подробнее в статье 1.2).</div>
            <div class="codex-sub"><i class="fas fa-chevron-right"></i> 1.1. Отменить договор можно при согласии всех членов правительства в течение 1 дня на мелкую сделку и 2 дней на крупную сделку.</div>
            <div class="codex-sub"><i class="fas fa-chevron-right"></i> 1.2. Если налоговой службе не понравится происхождение денег, выплаченных покупателем, то государство может отменить сделку (подробнее в статье 1.1.) и не выплачивать компенсацию покупателю. Государство может забрать эти деньги и вообще не отдавать их покупателю.</div>
        </div>
        <div class="codex-article">
            <div class="article-title"><i class="fas fa-car-crash"></i> 2. Нарушения на дороге</div>
            <div class="article-text">2. Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</div>
            <div class="codex-sub"><i class="fas fa-minus"></i> В первый раз — обязан выплатить штраф 10 рублей</div>
            <div class="codex-sub"><i class="fas fa-minus"></i> Во второй и следующие разы — выплачивает штраф и лишается свободы на срок 1 день</div>
            <div class="codex-sub" style="padding-left: 3rem; color: #b0cae5;"><i class="fas fa-info-circle"></i> *При лишении свободы деятельность человека прекращается на указанный срок.</div>
        </div>
        <div class="codex-article">
            <div class="article-title"><i class="fas fa-truck"></i> 3. При ДТП на дороге</div>
            <div class="codex-sub"><i class="fas fa-check-circle"></i> Вина — штраф оплачивает только виноватый участник</div>
            <div class="codex-sub"><i class="fas fa-check-circle"></i> Штраф виноватому — 5 000 рублей</div>
            <div class="codex-sub"><i class="fas fa-check-circle"></i> Пострадавшему — выплачивается компенсация 6 000 рублей</div>
            <div class="codex-sub"><i class="fas fa-check-circle"></i> Государству — выплаты не производятся</div>
            <div class="codex-sub" style="padding-left: 3rem; color: #b0cae5;"><i class="fas fa-info-circle"></i> *Без суда и решения штраф не выплачивается.</div>
        </div>
        <p style="margin-top: 1.2rem; color: #a7c2e0; font-size: 0.95rem; border-top: 1px solid #2f4a5f; padding-top: 1rem;"><i class="fas fa-asterisk" style="color: #f0c060;"></i> Кодекс вступает в силу с момента публикации и обязателен для всех граждан Республики «Team».</p>
    </div>

    <div class="passport-box section-scroll" id="passport">
        <h3><i class="fas fa-id-card"></i> Электронный паспорт</h3>
        <ul>
            <li><i class="fas fa-user"></i> Гражданин: <span id="passportName">Team-2026</span></li>
            <li><i class="fas fa-calendar-alt"></i> Дата регистрации: 01.01.2026</li>
            <li><i class="fas fa-shield-alt"></i> Статус: <span style="color: #6ee6b0;">активный</span></li>
            <li><i class="fas fa-fingerprint"></i> Цифровой ID: #T-0428</li>
        </ul>
        <div class="passport-id">
            <i class="fas fa-qrcode"></i>
            <span class="id-number">TEAM-2026-0X7F</span>
            <i class="fas fa-chevron-right" style="color: #4b9f7a;"></i>
        </div>
        <p style="margin-top: 0.8rem; font-size: 0.9rem; color: #9bb9db;"><i class="fas fa-sync-alt" style="color: #4edb9e;"></i> Действителен до: 01.01.2028</p>
    </div>

    <footer class="footer">
        <div class="footer-social">
            <a href="#"><i class="fab fa-discord"></i></a>
            <a href="#"><i class="fab fa-telegram-plane"></i></a>
            <a href="#"><i class="fab fa-github"></i></a>
            <a href="#"><i class="fab fa-youtube"></i></a>
        </div>
        <div class="footer-copy">
            <i class="fas fa-crown"></i>  Республика «Team» · 2026 · <i class="fas fa-code"></i> с командным духом
        </div>
    </footer>
</div>

<script>
    // ===== ДАННЫЕ АККАУНТОВ =====
    var users = {
        'Семён': { password: '135264', balance: 1000000 },
        'Азар': { password: '342567', balance: 0 },
        'Вика': { password: '845986', balance: 0 }
    };

    var currentUser = null;

    // ===== ПЕРЕНОС К РАЗДЕЛАМ =====
    function scrollToSection(id) {
        var el = document.getElementById(id);
        if (el) {
            var top = el.getBoundingClientRect().top + window.pageYOffset - 80;
            window.scrollTo({ top: top, behavior: 'smooth' });
        }
    }

    // ===== АВТОРИЗАЦИЯ =====
    function showLogin() {
        if (currentUser) return;
        document.getElementById('loginForm').classList.add('active');
        document.getElementById('loginError').classList.remove('show');
        document.getElementById('loginUser').value = '';
        document.getElementById('loginPass').value = '';
        setTimeout(function() { document.getElementById('loginUser').focus(); }, 100);
    }

    function hideLogin() {
        document.getElementById('loginForm').classList.remove('active');
    }

    function doLogin() {
        var login = document.getElementById('loginUser').value.trim();
        var pass = document.getElementById('loginPass').value.trim();

        if (users[login] && users[login].password === pass) {
            currentUser = login;
            document.getElementById('loginForm').classList.remove('active');
            updateUI();
        } else {
            document.getElementById('loginError').classList.add('show');
        }
    }

    function logout() {
        currentUser = null;
        updateUI();
    }

    function updateUI() {
        var greeting = document.getElementById('greeting');
        var loginBtn = document.getElementById('loginBtn');
        var nameDisplay = document.getElementById('userName');
        var passportName = document.getElementById('passportName');
        var balanceDisplay = document.getElementById('balanceDisplay');
        var financeOwner = document.getElementById('financeOwner');

        if (currentUser) {
            greeting.style.display = 'flex';
            loginBtn.style.display = 'none';
            nameDisplay.textContent = currentUser;
            passportName.textContent = currentUser + ' (гражданин)';
            financeOwner.textContent = currentUser;
            // Показываем баланс
            var bal = users[currentUser].balance;
            balanceDisplay.textContent = bal.toLocaleString('ru-RU');
        } else {
            greeting.style.display = 'none';
            loginBtn.style.display = 'inline-flex';
            passportName.textContent = 'Team-2026';
            financeOwner.textContent = 'Гость';
            balanceDisplay.textContent = '0';
        }
    }

    // ===== ОБРАБОТЧИКИ =====
    document.addEventListener('DOMContentLoaded', function() {
        document.getElementById('loginUser').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') { e.preventDefault(); doLogin(); }
        });
        document.getElementById('loginPass').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') { e.preventDefault(); doLogin(); }
        });
    });
</script>
</body>
</html>

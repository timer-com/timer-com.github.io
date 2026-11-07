

<!DOCTYPE html>
<html lang="ru">
<head>
<script>(function(){function fmt(a){if(a instanceof Error)return a.message;if(typeof a==="object"&&a!==null){try{return JSON.stringify(a)}catch(e){return String(a)}}return String(a)}function send(t,m,l){try{parent.postMessage({__stc:1,type:t,msg:m,line:l},"*")}catch(e){}}["log","info","warn","error"].forEach(function(m){var o=console[m];console[m]=function(){send(m,Array.prototype.map.call(arguments,fmt).join(" "));if(o)o.apply(console,arguments)}});window.addEventListener("error",function(e){send("error",e.message,e.lineno)});window.addEventListener("unhandledrejection",function(e){send("error","Promise: "+fmt(e.reason))});})();</script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer-Community — Сообщество программистов</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; scroll-behavior: smooth; }
        :root { --bg: #0b0c10; --card: #1f2833; --alt-bg: #12141c; --neon: #4ed5ff; --hover: #00a8e8; --txt: #c5c6c7; --glow: rgba(78, 213, 255, 0.3); }
        body { background: var(--bg); color: var(--txt); line-height: 1.6; }
        .container { width: 90%; max-width: 1200px; margin: 0 auto; }
        
        header { padding: 20px 0; border-bottom: 1px solid var(--card); position: sticky; top: 0; background: rgba(11, 12, 16, 0.95); backdrop-filter: blur(10px); z-index: 100; }
        .nav-box { display: flex; justify-content: space-between; align-items: center; }
        .logo { font-size: 24px; font-weight: 800; color: #fff; letter-spacing: 0.5px; }
        .logo span, .sec-title span { color: var(--neon); text-shadow: 0 0 10px var(--glow); }
        .menu { list-style: none; display: flex; gap: 25px; }
        .menu a { color: var(--txt); text-decoration: none; font-weight: 500; transition: 0.3s; }
        .menu a:hover { color: var(--neon); }

        .hero { padding: 120px 0 80px; text-align: center; }
        .hero h1 { color: #fff; font-size: 3.5rem; font-weight: 800; margin-bottom: 20px; line-height: 1.2; }
        .hero h1 span { color: var(--neon); text-shadow: 0 0 15px var(--glow); }
        .hero p { font-size: 1.25rem; max-width: 750px; margin: 0 auto 40px; color: #909090; }
        
        .btn { display: inline-block; background: var(--neon); color: #0b0c10; padding: 15px 32px; border-radius: 8px; text-decoration: none; font-weight: 700; box-shadow: 0 4px 20px var(--glow); transition: 0.3s; }
        .btn:hover { background: var(--hover); transform: translateY(-2px); box-shadow: 0 6px 25px rgba(78, 213, 255, 0.5); }
        .btn-sec { background: transparent; color: var(--neon); border: 2px solid var(--neon); padding: 10px 24px; border-radius: 6px; text-decoration: none; font-weight: 600; transition: 0.3s; display: inline-block; margin-top: 15px; }
        .btn-sec:hover { background: var(--neon); color: #0b0c10; }

        .section { padding: 80px 0; margin-bottom: 40px; }
        .sec-alt { background: var(--alt-bg); border-radius: 20px; }
        .sec-title { text-align: center; color: #fff; font-size: 2.2rem; margin-bottom: 50px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        
        .card { background: var(--bg); padding: 40px 30px; border-radius: 12px; border: 1px solid var(--card); transition: 0.3s; }
        .card:hover { transform: translateY(-5px); border-color: var(--neon); box-shadow: 0 10px 20px rgba(0,0,0,0.3); }
        .card-icon { font-size: 2.5rem; margin-bottom: 20px; display: inline-block; }
        .card h3 { color: #fff; margin-bottom: 15px; font-size: 1.35rem; }
        
        .p-card { background: var(--card); max-width: 600px; margin: 0 auto; border: 1px solid #2e3c4e; text-align: center; }
        .e-card { background: var(--card); border-left: 4px solid var(--neon); padding: 30px; border-radius: 8px; max-width: 700px; margin: 0 auto; text-align: center; }
        .e-date { display: inline-block; background: rgba(78, 213, 255, 0.1); color: var(--neon); padding: 6px 16px; border-radius: 20px; font-weight: 700; margin-bottom: 15px; font-size: 0.9rem; }
        
        footer { background: #050508; padding: 50px 0; border-top: 1px solid var(--card); text-align: center; font-size: 0.95rem; }
        footer p { margin-bottom: 15px; }
        .meta { color: #666; font-size: 0.85rem; margin-top: 15px; }
        @media (max-width: 768px) { .hero h1 { font-size: 2.4rem; } .menu { display: none; } }
    </style>
</head>
<body>

    <header>
        <div class="container nav-box">
            <div class="logo">Timer<span>-Community</span></div>
            <nav><ul class="menu">
                <li><a href="#about">О нас</a></li>
                <li><a href="#projects">Проекты</a></li>
                <li><a href="#events">События</a></li>
                <li><a href="https://max.ru/join/c0gw5A2kaMc6qBLcLiXlO52MoWKMVyFvMC9I5UwZTVo" target="_blank">Наш канал</a></li>
            </ul></nav>
        </div>
    </header>

    <section class="hero">
        <div class="container">
            <h1>Добро пожаловать в <span>Timer-Community</span></h1>
            <p>Мы объединяем опытных разработчиков и амбициозных новичков для создания крутых совместных проектов. Растем и пишем код вместе!</p>
            <a href="https://max.ru/join/c0gw5A2kaMc6qBLcLiXlO52MoWKMVyFvMC9I5UwZTVo" target="_blank" class="btn">Стать частью команды</a>
        </div>
    </section>

    <section class="section sec-alt" id="about">
        <div class="container">
            <h2 class="sec-title">Почему выбирают <span>наше комьюнити</span>?</h2>
            <div class="grid">
                <div class="card">
                    <span class="card-icon">💻</span>
                    <h3>Совместные проекты</h3>
                    <p>Наша главная фишка — командная разработка. Мы объединяем усилия, чтобы создавать реальные IT-продукты, делиться опытом и собирать мощные портфолио.</p>
                </div>
                <div class="card">
                    <span class="card-icon">❤️</span>
                    <h3>Уважение к труду</h3>
                    <p>В Timer-Community ценится вклад каждого участника. Мы уважаем время, усилия и идеи, которые программисты вкладывают в общее дело.</p>
                </div>
                <div class="card">
                    <span class="card-icon">🚀</span>
                    <h3>Рады новичкам</h3>
                    <p>Мы примем любого, у кого горят глаза! Наша главная задача — объединить лучших профессионалов и тех, кто только начинает свой путь в программировании.</p>
                </div>
            </div>
        </div>
    </section>

    <section class="section" id="projects">
        <div class="container">
            <h2 class="sec-title">Наши <span>Разработки</span></h2>
            <div class="card p-card">
                <span class="card-icon">🔱</span>
                <h3>Triton Programming Language</h3>
                <p>Высокоуровневый интерактивный язык программирования с русскоязычным синтаксисом. Создан для быстрого прототипирования, легкого обучения алгоритмам и выполнения скриптов прямо в браузере.</p>
                <a href="https://github.com/timer-com/TC-Triton.programming-languge" target="_blank" class="btn-sec">Исходный код на GitHub</a>
            </div>
        </div>
    </section>

    <section class="section sec-alt" id="events">
        <div class="container">
            <h2 class="sec-title">Предстоящие <span>События</span></h2>
            <div class="e-card">
                <span class="e-date">📅 21 января 2027 года</span>
                <h3>Математическая олимпиада «Высший уровень»</h3>
                <p>Совсем скоро наше сообщество проведет масштабное интеллектуальное соревнование! Проверьте свои силы в логике, нестандартном мышлении и алгоритмической математике. Следите за анонсами в нашем канале, чтобы не пропустить регистрацию.</p>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <p><strong>Timer-Community</strong> — Пишем код будущего вместе.</p>
            <a href="https://max.ru/join/c0gw5A2kaMc6qBLcLiXlO52MoWKMVyFvMC9I5UwZTVo" target="_blank" class="btn" style="padding: 10px 24px; font-size: 0.9rem;">Вступить в Макс</a>
            <p class="meta">Основано: 31 декабря 2025 года | Создатель и владелец: <strong>Timer</strong></p>
            <p class="meta" style="margin-top: 5px;">&copy; 2026 Все права защищены.</p>
        </div>
    </footer>

    </body>
 </html>

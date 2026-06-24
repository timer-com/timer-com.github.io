
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Официальный сайт Тимер-community · Магазин</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: 'Quicksand', sans-serif;
      background: linear-gradient(145deg, #f9f3e6 0%, #fff9f0 100%);
      color: #2d3e4b;
      padding: 2rem 1.5rem;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .container {
      max-width: 1300px;
      width: 100%;
    }

    /* Заголовок сайта */
    .site-title {
      text-align: center;
      margin-bottom: 2rem;
    }
    .site-title h1 {
      font-size: 2.2rem;
      font-weight: 700;
      color: #4b6b7a;
      letter-spacing: 0.5px;
    }
    .site-title h1 i {
      color: #dba56d;
      margin-right: 8px;
    }
    .site-title .sub {
      font-size: 0.9rem;
      color: #7a9aaa;
      font-weight: 600;
    }

    /* сетка карточек */
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
      gap: 2rem;
      margin: 0.5rem 0 2rem;
    }

    .card {
      background: rgba(255, 248, 235, 0.7);
      backdrop-filter: blur(4px);
      padding: 1.8rem 1.2rem 1.8rem;
      border-radius: 48px 20px 48px 20px;
      box-shadow: 0 20px 40px -12px rgba(210, 170, 120, 0.25),
                  inset 0 1px 4px #fff5e6;
      border: 1px solid #fff4e0;
      transition: 0.2s ease-in;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
    }

    .card:hover {
      transform: translateY(-8px);
      background: #fffbf2;
      box-shadow: 0 30px 50px -16px #dbbd9b;
      border-color: #fad49e;
    }

    .card-icon {
      font-size: 2.8rem;
      margin-bottom: 0.6rem;
      background: #ffedd6;
      padding: 0.4rem 0.8rem;
      border-radius: 60px;
      color: #9b7b5e;
    }

    .card h3 {
      font-size: 1.5rem;
      font-weight: 700;
      color: #3b5a69;
      margin: 0.2rem 0 0.3rem;
    }

    .card .sub {
      font-weight: 600;
      color: #be8f64;
      font-size: 0.8rem;
      letter-spacing: 0.4px;
      text-transform: uppercase;
      background: #fae9d4;
      padding: 0.1rem 0.7rem;
      border-radius: 50px;
      display: inline-block;
      margin-bottom: 0.6rem;
    }

    .card p {
      font-size: 0.95rem;
      line-height: 1.5;
      color: #3b4f5a;
      margin: 0.6rem 0 0.8rem;
      opacity: 0.9;
    }

    .price-tag {
      background: #ffdcaa;
      padding: 0.3rem 1rem;
      border-radius: 60px;
      font-weight: 700;
      color: #2e4a55;
      font-size: 1rem;
      margin-top: auto;
      align-self: flex-start;
      box-shadow: 0 2px 6px rgba(236, 170, 80, 0.3);
    }

    .card .btn, .special-card .btn {
      margin-top: 0.8rem;
      border: none;
      padding: 0.6rem 1.5rem;
      border-radius: 60px;
      font-weight: 700;
      color: #2d3d45;
      font-size: 0.9rem;
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      transition: 0.15s;
      cursor: pointer;
      box-shadow: 0 4px 8px rgba(190, 140, 80, 0.15);
      border: 1px solid #f5dbb5;
      background: #f5dbb5;
      text-decoration: none;
      font-family: inherit;
    }

    .card .btn i, .special-card .btn i {
      font-size: 1rem;
    }

    .card .btn:hover, .special-card .btn:hover {
      background: #eaccaa;
      transform: scale(1.02);
      border-color: #c8a97e;
    }

    .detail-list {
      font-size: 0.85rem;
      list-style: none;
      padding: 0;
      margin: 0.2rem 0 0.4rem;
      color: #3f5a63;
    }
    .detail-list li {
      padding: 0.1rem 0;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .detail-list li i {
      color: #c29a6b;
      width: 16px;
      font-size: 0.7rem;
    }

    .highlight-box {
      background: #fff2e0;
      border-radius: 16px;
      padding: 0.5rem 0.8rem;
      margin: 0.3rem 0 0.5rem;
      border-left: 4px solid #dba56d;
      font-size: 0.9rem;
      line-height: 1.5;
      width: 100%;
    }
    .highlight-box i {
      color: #b48f6b;
      margin-right: 6px;
    }

    /* Секция "особенные" — фрукты / brainrot */
    .special-row {
      display: flex;
      flex-wrap: wrap;
      gap: 2rem;
      margin-top: 1.5rem;
      margin-bottom: 1.5rem;
      justify-content: center;
    }

    .special-card {
      background: #fffaee;
      border-radius: 60px 20px 60px 20px;
      padding: 1.8rem 2rem;
      flex: 1 1 280px;
      box-shadow: 0 16px 32px -8px #dac09a;
      border: 1px solid #ffe5c6;
      transition: 0.2s;
      display: flex;
      flex-direction: column;
    }

    .special-card:hover {
      background: #fff7e7;
      border-color: #fbcb8e;
      transform: scale(1.01);
    }

    .special-card .top {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .special-card .top i {
      font-size: 3rem;
      color: #ad7d54;
      background: #fbe5cd;
      padding: 0.5rem;
      border-radius: 50px;
    }

    .special-card h3 {
      font-size: 1.8rem;
      font-weight: 700;
      color: #3c5c66;
    }

    .special-card .price {
      background: #f7dbb6;
      padding: 0.2rem 1.2rem;
      border-radius: 40px;
      font-weight: 700;
      font-size: 1.2rem;
      align-self: flex-start;
      margin: 0.8rem 0 0.2rem;
    }

    .special-card .desc {
      font-size: 1rem;
      color: #475f69;
      margin: 0.4rem 0 0.2rem;
    }

    .badge {
      background: #b5d6c9;
      color: #1f3a40;
      padding: 0.1rem 0.9rem;
      border-radius: 60px;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      display: inline-block;
      margin-top: 0.2rem;
    }

    .section-title {
      margin: 0.5rem 0 0.2rem;
    }
    .section-title span {
      background: #eccea9;
      padding: 0.3rem 1.8rem;
      border-radius: 60px;
      font-weight: 700;
      font-size: 1.2rem;
      color: #2e4a4f;
      display: inline-block;
    }

    /* Блок контактов — якорь */
    #contacts {
      scroll-margin-top: 20px;
    }

    .contacts-block {
      margin: 2.5rem 0 1rem;
      padding: 1.8rem 2rem;
      background: #fffbf2;
      border-radius: 60px 20px 60px 20px;
      border: 2px solid #f5dec6;
      box-shadow: 0 12px 28px -8px #dac09a;
      text-align: center;
      transition: 0.3s;
    }
    .contacts-block.highlight {
      border-color: #dba56d;
      box-shadow: 0 0 0 4px #f5dbb5, 0 12px 28px -8px #dac09a;
    }
    .contacts-block h2 {
      font-size: 1.6rem;
      font-weight: 700;
      color: #3b5a69;
      margin-bottom: 0.5rem;
    }
    .contacts-block h2 i {
      color: #dba56d;
      margin-right: 10px;
    }
    .contacts-block .contact-email {
      font-size: 1.5rem;
      font-weight: 700;
      color: #4b6b7a;
      background: #fae9d4;
      padding: 0.4rem 2rem;
      border-radius: 60px;
      display: inline-block;
      margin-top: 0.3rem;
      border: 2px dashed #dba56d;
    }
    .contacts-block .contact-email i {
      color: #b48f6b;
      margin-right: 10px;
    }
    .contacts-block .contact-desc {
      font-size: 1rem;
      color: #4d6b78;
      margin-top: 0.5rem;
      font-weight: 600;
    }
    .contacts-block .contact-desc i {
      color: #c29a6b;
      margin: 0 4px;
    }

    /* Блок со ссылкой на канал в Max */
    .max-channel {
      margin: 1.5rem 0 1rem;
      padding: 1.5rem;
      background: linear-gradient(135deg, #fff2e0, #ffe8d0);
      border-radius: 60px 20px 60px 20px;
      border: 2px solid #f5dec6;
      text-align: center;
      box-shadow: 0 8px 20px -6px #dac09a;
    }
    .max-channel .channel-link {
      display: inline-block;
      font-size: 1.4rem;
      font-weight: 700;
      color: #3b5a69;
      background: white;
      padding: 0.6rem 2rem;
      border-radius: 60px;
      text-decoration: none;
      border: 2px solid #dba56d;
      transition: 0.2s;
      box-shadow: 0 4px 12px rgba(219, 165, 109, 0.25);
    }
    .max-channel .channel-link i {
      color: #dba56d;
      margin-right: 10px;
    }
    .max-channel .channel-link:hover {
      background: #f5e4cf;
      transform: scale(1.02);
      border-color: #c29a6b;
    }
    .max-channel .channel-label {
      font-size: 1.1rem;
      font-weight: 600;
      color: #4d6b78;
      margin-bottom: 0.5rem;
    }
    .max-channel .channel-label i {
      color: #dba56d;
      margin-right: 6px;
    }

    .extra-prices {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      justify-content: center;
      margin: 1rem 0 0.5rem;
    }
    .extra-prices div {
      background: #fff6ea;
      border-radius: 40px;
      padding: 0.4rem 1.8rem;
      border: 1px solid #eddcc8;
      font-size: 0.9rem;
    }
    .extra-prices i {
      color: #b48f6b;
      margin-right: 4px;
    }

    @media (max-width: 700px) {
      .grid {
        grid-template-columns: 1fr;
      }
      .contacts-block .contact-email {
        font-size: 1.1rem;
        padding: 0.3rem 1rem;
      }
      .max-channel .channel-link {
        font-size: 1.1rem;
        padding: 0.4rem 1.2rem;
      }
    }
  </style>
</head>
<body>
<div class="container">

  <!-- ЗАГОЛОВОК САЙТА -->
  <div class="site-title">
    <h1><i class="fas fa-crown"></i> Официальный сайт Тимер-community</h1>
    <div class="sub"><i class="fas fa-store"></i> Магазин услуг — Roblox, код, сайты</div>
  </div>

  <!-- ============ МАГАЗИН ============ -->

  <div class="grid">

    <!-- Robux -->
    <div class="card">
      <div class="card-icon"><i class="fab fa-roblox"></i></div>
      <h3>Robux</h3>
      <span class="sub">пополнение</span>
      <p><strong>1 ₽ = 0.75 Robux</strong> · Пополнение от <strong>1 до 300 Robux</strong>.</p>
      <div class="highlight-box">
        <i class="fas fa-hand-holding-usd"></i> <strong>Через Pls Donate</strong><br>
        <span style="font-size: 0.85rem;">Срок — <strong>до 1 недели</strong>.<br>Зависит от возможности захода на плейс как покупателя, так и продавца.</span>
      </div>
      <ul class="detail-list">
        <li><i class="fas fa-arrow-right"></i> 10 Robux ≈ 14 ₽</li>
        <li><i class="fas fa-arrow-right"></i> 100 Robux ≈ 134 ₽</li>
        <li><i class="fas fa-arrow-right"></i> 300 Robux ≈ 400 ₽</li>
      </ul>
      <div class="price-tag">от 14 ₽</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-bolt"></i> Купить Robux</button>
    </div>

    <!-- Scratch -->
    <div class="card">
      <div class="card-icon"><i class="fas fa-cat"></i></div>
      <h3>Scratch</h3>
      <span class="sub">проекты</span>
      <ul class="detail-list">
        <li><i class="fas fa-star" style="color: #7ab07a;"></i> Лёгкий — <strong>25 ₽</strong></li>
        <li><i class="fas fa-star" style="color: #d4a373;"></i> Сложный — <strong>50 ₽</strong></li>
        <li><i class="fas fa-star" style="color: #b87333;"></i> Очень сложный — <strong>100 ₽</strong></li>
      </ul>
      <p style="font-size: 0.9rem;">Игры, анимации, интерактив. Любая тема.</p>
      <div class="price-tag">от 25 ₽</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-paint-brush"></i> Заказать Scratch</button>
    </div>

    <!-- HTML -->
    <div class="card">
      <div class="card-icon"><i class="fab fa-html5"></i></div>
      <h3>HTML / CSS</h3>
      <span class="sub">коды</span>
      <ul class="detail-list">
        <li><i class="fas fa-code"></i> Лёгкий (лендинг) — <strong>25 ₽</strong></li>
        <li><i class="fas fa-code"></i> Сложный (сайт 3-5 стр) — <strong>50 ₽</strong></li>
        <li><i class="fas fa-code"></i> Очень сложный (анимации, JS) — <strong>100 ₽</strong></li>
      </ul>
      <p style="font-size: 0.9rem;">Адаптив, чистый код, с пояснениями.</p>
      <div class="price-tag">от 25 ₽</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-laptop-code"></i> Получить HTML</button>
    </div>

    <!-- Python -->
    <div class="card">
      <div class="card-icon"><i class="fab fa-python"></i></div>
      <h3>Python</h3>
      <span class="sub">скрипты</span>
      <ul class="detail-list">
        <li><i class="fas fa-robot"></i> Лёгкий (парсер) — <strong>25 ₽</strong></li>
        <li><i class="fas fa-robot"></i> Сложный (бот/API) — <strong>50 ₽</strong></li>
        <li><i class="fas fa-robot"></i> Очень сложный (нейросеть) — <strong>100 ₽</strong></li>
      </ul>
      <p style="font-size: 0.9rem;">Готовые скрипты под ваш запрос.</p>
      <div class="price-tag">от 25 ₽</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-terminal"></i> Заказать Python</button>
    </div>

    <!-- Аренда сайтов -->
    <div class="card">
      <div class="card-icon"><i class="fas fa-globe"></i></div>
      <h3>Аренда сайтов</h3>
      <span class="sub">256 ₽ / месяц</span>
      <div class="highlight-box">
        <i class="fas fa-info-circle"></i> <strong>Условия:</strong><br>
        • Покупатель присылает <strong>описание</strong> желаемого сайта.<br>
        • После окончания аренды сайт <strong>удаляется</strong>.<br>
        • Сайт делается любой сложности по описанию.
      </div>
      <ul class="detail-list">
        <li><i class="fas fa-calendar"></i> 1 месяц — <strong>256 ₽</strong></li>
        <li><i class="fas fa-calendar"></i> 3 месяца — <strong>700 ₽</strong></li>
        <li><i class="fas fa-calendar"></i> 6 месяцев — <strong>1300 ₽</strong></li>
      </ul>
      <div class="price-tag">256 ₽/мес</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-server"></i> Арендовать</button>
    </div>

    <!-- Полная покупка сайта -->
    <div class="card">
      <div class="card-icon"><i class="fas fa-pen-fancy"></i></div>
      <h3>Купить сайт</h3>
      <span class="sub">полностью</span>
      <div class="highlight-box">
        <i class="fas fa-check-circle"></i> <strong>2200 ₽ — любой сайт</strong><br>
        <span style="font-size: 0.9rem;">Абсолютно любой сайт по желанию покупателя.<br>Разработка под ключ, без ограничений.</span>
      </div>
      <ul class="detail-list">
        <li><i class="fas fa-crown"></i> Сайт остаётся у вас навсегда</li>
        <li><i class="fas fa-crown"></i> Любая сложность и тематика</li>
      </ul>
      <div class="price-tag">2200 ₽</div>
      <button class="btn scroll-to-contacts"><i class="fas fa-rocket"></i> Заказать сайт</button>
    </div>
  </div>

  <!-- СПЕЦИАЛЬНЫЕ УСЛУГИ -->
  <div class="section-title">
    <span><i class="fas fa-seedling" style="margin-right: 10px;"></i> Из Roblox — договорная цена</span>
  </div>

  <div class="special-row">
    <!-- Grow a Garden -->
    <div class="special-card">
      <div class="top">
        <i class="fas fa-apple-alt"></i>
        <h3>Grow a Garden</h3>
      </div>
      <div class="desc"><i class="fas fa-leaf" style="color: #6b8c4d;"></i> Фрукты / ягоды / овощи</div>
      <div class="price">💬 договорная</div>
      <div class="highlight-box" style="border-left-color: #6b8c4d; background: #f0f7e8;">
        <i class="fas fa-ticket-alt"></i> <strong>Получение:</strong> через <strong>trading ticket</strong>.<br>
        <span style="font-size: 0.85rem;">Цена и товар обсуждаются с продавцом индивидуально.</span>
      </div>
      <ul class="detail-list">
        <li><i class="fas fa-check"></i> Любые фрукты из игры</li>
        <li><i class="fas fa-check"></i> Доставка в личный аккаунт</li>
      </ul>
      <div class="badge"><i class="fas fa-handshake"></i> договорная цена</div>
      <button class="btn scroll-to-contacts" style="background: #c8d9b0; border-color: #b0c99a;"><i class="fas fa-comment-dollar"></i> Обсудить цену</button>
    </div>

    <!-- Steal a Brainrot -->
    <div class="special-card">
      <div class="top">
        <i class="fas fa-brain"></i>
        <h3>Steal a Brainrot</h3>
      </div>
      <div class="desc"><i class="fas fa-skull" style="color: #a07554;"></i> Браинроты / мозги</div>
      <div class="price">💬 договорная</div>
      <div class="highlight-box" style="border-left-color: #a07554; background: #f5ede7;">
        <i class="fas fa-database"></i> <strong>Получение:</strong> покупатель забирает товар <strong>с базы продавца</strong>.<br>
        <span style="font-size: 0.85rem;">Цена и ассортимент обсуждаются индивидуально.</span>
      </div>
      <ul class="detail-list">
        <li><i class="fas fa-star" style="color: #f5b342;"></i> Редкие и легендарные варианты</li>
        <li><i class="fas fa-star" style="color: #f5b342;"></i> Самостоятельный забор с базы</li>
      </ul>
      <div class="badge"><i class="fas fa-handshake"></i> договорная цена</div>
      <button class="btn scroll-to-contacts" style="background: #dbc1b0; border-color: #c9ac98;"><i class="fas fa-comment-dollar"></i> Обсудить цену</button>
    </div>
  </div>

  <!-- ============ БЛОК КОНТАКТОВ (ЯКОРЬ) ============ -->
  <div id="contacts" class="contacts-block">
    <h2><i class="fas fa-envelope"></i> Контакты для заказов</h2>
    <div class="contact-email">
      <i class="fas fa-at"></i> timer.com484@gmail.com
    </div>
    <div class="contact-desc">
      <i class="fas fa-pen"></i> По всем заказам и вопросам писать сюда <i class="fas fa-arrow-right"></i>
      <span style="background: #f5e4cf; padding: 0.1rem 1rem; border-radius: 40px; font-weight: 700;">timer.com484@gmail.com</span>
    </div>
    <div style="margin-top: 0.5rem; font-size: 0.9rem; color: #6b8b9c;">
      <i class="fas fa-clock"></i> Отвечаем в течение 24 часов
    </div>
  </div>

  <!-- ============ ССЫЛКА НА КАНАЛ В MAX ============ -->
  <div class="max-channel">
    <div class="channel-label">
      <i class="fas fa-broadcast-tower"></i> Наш канал в Max
    </div>
    <a href="https://max.ru/join/XOwp5TOPv0W-dqYNgy6mLc4DOKP4KmvmQ7C7ZSputR4" target="_blank" class="channel-link">
      <i class="fas fa-external-link-alt"></i> Перейти в канал
    </a>
  </div>

  <!-- Дополнительные цены -->
  <div class="extra-prices">
    <div><i class="fas fa-cubes"></i> Аренда сайтов <strong>256 ₽/мес</strong></div>
    <div><i class="fas fa-laptop-code"></i> HTML / Python <strong>от 25 ₽</strong></div>
    <div><i class="fas fa-gamepad"></i> Robux: 1₽ = 0.75 Robux (1–300)</div>
    <div><i class="fas fa-crown"></i> Сайт под ключ <strong>2200 ₽</strong></div>
  </div>

</div>

<!-- Скрипт для плавной прокрутки к контактам -->
<script>
  (function() {
    const buttons = document.querySelectorAll('.scroll-to-contacts');
    const contactsBlock = document.getElementById('contacts');

    if (!contactsBlock) return;

    buttons.forEach(function(btn) {
      btn.addEventListener('click', function(e) {
        e.preventDefault();

        contactsBlock.scrollIntoView({
          behavior: 'smooth',
          block: 'start'
        });

        setTimeout(function() {
          contactsBlock.classList.add('highlight');
          setTimeout(function() {
            contactsBlock.classList.remove('highlight');
          }, 1500);
        }, 400);
      });
    });
  })();
</script>

</body>
</html>

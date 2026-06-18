<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🐚 Тритон — Русский язык программирования</title>
    <style>
        /* ============================================================
           ВСЕ СТИЛИ
           ============================================================ */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background: #0a0e17;
            color: #e0e0e0;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* ============================================================
           ШАПКА С ЛОГОТИПОМ (НЕУБИРАЕМЫЙ)
           ============================================================ */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
            padding: 20px 0;
            border-bottom: 1px solid #1a2a40;
            margin-bottom: 20px;
            background: #0f1625;
            border-radius: 12px;
            padding: 15px 25px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.5em;
            font-weight: 700;
            /* НЕЛЬЗЯ УБРАТЬ - логотип встроен в код! */
            user-select: none;
            -webkit-user-select: none;
        }

        /* ============================================================
           ОСНОВНОЙ ЛОГОТИП — ВСТРОЕННЫЙ SVG
           ============================================================ */
        .logo svg {
            width: 50px;
            height: 50px;
            flex-shrink: 0;
            /* Запрещаем изменение размера */
            filter: drop-shadow(0 0 10px rgba(123, 47, 252, 0.3));
            transition: filter 0.3s;
        }

        .logo svg:hover {
            filter: drop-shadow(0 0 20px rgba(123, 47, 252, 0.6));
        }

        /* Альтернативный вариант - если хочешь картинку, раскомментируй и закомментируй SVG выше */
        /*
        .logo img {
            width: 50px;
            height: 50px;
            border-radius: 8px;
            object-fit: contain;
            flex-shrink: 0;
        }
        */

        .logo-text {
            background: linear-gradient(135deg, #00d4ff, #7b2ffc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-size: 1.3em;
            letter-spacing: 1px;
        }

        .logo-badge {
            background: #1a4a3a;
            color: #7bed9f;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.6em;
            border: 1px solid #2a5a4a;
            font-weight: 600;
            letter-spacing: 0.5px;
            margin-left: 5px;
        }

        /* Правый блок шапки */
        .header-right {
            display: flex;
            align-items: center;
            gap: 15px;
            flex-wrap: wrap;
        }

        .header-right .info {
            color: #5a6a8a;
            font-size: 0.85em;
        }

        .header-right .info span {
            color: #7b2ffc;
            font-weight: 600;
        }

        /* ============================================================
           ВКЛАДКИ
           ============================================================ */
        .tabs {
            display: flex;
            gap: 5px;
            margin-bottom: 20px;
            border-bottom: 2px solid #1a2a40;
        }

        .tab-btn {
            padding: 12px 30px;
            background: transparent;
            border: none;
            color: #5a6a8a;
            font-size: 1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            border-bottom: 3px solid transparent;
            border-radius: 8px 8px 0 0;
        }

        .tab-btn:hover {
            color: #c8d0e0;
            background: #0f1625;
        }

        .tab-btn.active {
            color: #00d4ff;
            border-bottom-color: #7b2ffc;
            background: #0f1625;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ============================================================
           РЕДАКТОР
           ============================================================ */
        .main-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            min-height: 500px;
        }

        @media (max-width: 900px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
        }

        .panel {
            background: #0f1625;
            border: 1px solid #1a2a40;
            border-radius: 12px;
            padding: 15px;
            display: flex;
            flex-direction: column;
        }

        .panel-label {
            color: #7b8baa;
            font-size: 0.85em;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        textarea {
            flex: 1;
            background: #0a0e17;
            color: #c8d0e0;
            border: 1px solid #1a2a40;
            border-radius: 8px;
            padding: 15px;
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 14px;
            line-height: 1.7;
            resize: vertical;
            outline: none;
            min-height: 400px;
        }

        textarea:focus {
            border-color: #7b2ffc;
        }

        .output {
            flex: 1;
            background: #0a0e17;
            border-radius: 8px;
            padding: 15px;
            border: 1px solid #1a2a40;
            overflow-y: auto;
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 14px;
            line-height: 1.8;
            min-height: 400px;
            white-space: pre-wrap;
            word-wrap: break-word;
        }

        .output .log {
            color: #7bed9f;
        }
        .output .error {
            color: #ff6b6b;
        }
        .output .info {
            color: #ffd93d;
        }
        .output .system {
            color: #7b9fff;
        }

        .toolbar {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 10px 0;
        }

        .btn {
            padding: 10px 24px;
            border: none;
            border-radius: 8px;
            font-size: 0.95em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-run {
            background: linear-gradient(135deg, #7b2ffc, #00d4ff);
            color: white;
            box-shadow: 0 4px 15px rgba(123, 47, 252, 0.3);
        }

        .btn-run:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(123, 47, 252, 0.5);
        }

        .btn-clear {
            background: #1a2a40;
            color: #7b8baa;
        }

        .btn-clear:hover {
            background: #2a3a5a;
            color: #c8d0e0;
        }

        .btn-example {
            background: #1a2a40;
            color: #7b8baa;
        }

        .btn-example:hover {
            background: #2a3a5a;
            color: #c8d0e0;
        }

        .btn-save {
            background: #1a4a3a;
            color: #7bed9f;
            border: 1px solid #2a5a4a;
        }

        .btn-save:hover {
            background: #2a5a4a;
            transform: translateY(-2px);
        }

        .btn-load {
            background: #1a3a5a;
            color: #7b9fff;
            border: 1px solid #2a4a6a;
        }

        .btn-load:hover {
            background: #2a4a6a;
            transform: translateY(-2px);
        }

        .status-bar {
            color: #5a6a8a;
            font-size: 0.85em;
            padding: 10px 0;
            border-top: 1px solid #1a2a40;
            margin-top: 10px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }

        /* ============================================================
           ДОКУМЕНТАЦИЯ
           ============================================================ */
        .doc-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 15px;
            padding: 10px 0;
        }

        .doc-card {
            background: #0f1625;
            border: 1px solid #1a2a40;
            border-radius: 10px;
            padding: 15px;
            transition: all 0.3s;
        }

        .doc-card:hover {
            border-color: #7b2ffc;
            transform: translateY(-3px);
        }

        .doc-card .cmd {
            color: #ffd93d;
            font-family: 'Consolas', monospace;
            font-size: 1.1em;
            font-weight: 700;
        }

        .doc-card .cmd .kw {
            color: #7b2ffc;
        }

        .doc-card .desc {
            color: #8899bb;
            font-size: 0.92em;
            margin: 8px 0 10px;
        }

        .doc-card .example {
            background: #0a0e17;
            border-radius: 4px;
            padding: 10px;
            font-family: 'Consolas', monospace;
            font-size: 0.8em;
            color: #c8d0e0;
            border-left: 3px solid #00d4ff;
            overflow-x: auto;
            white-space: pre-wrap;
        }

        .doc-card .tags {
            display: flex;
            gap: 5px;
            flex-wrap: wrap;
            margin-top: 8px;
        }

        .doc-card .tag {
            background: #1a2a40;
            color: #7b8baa;
            padding: 2px 10px;
            border-radius: 20px;
            font-size: 0.65em;
        }

        .doc-card .tag.primary {
            background: #2a1a4a;
            color: #b07bff;
        }

        .doc-search {
            margin-bottom: 15px;
            display: flex;
            gap: 10px;
        }

        .doc-search input {
            flex: 1;
            padding: 10px 20px;
            background: #0a0e17;
            border: 1px solid #1a2a40;
            border-radius: 8px;
            color: #c8d0e0;
            font-size: 1em;
            outline: none;
        }

        .doc-search input:focus {
            border-color: #7b2ffc;
        }

        .doc-count {
            color: #5a6a8a;
            font-size: 0.85em;
            padding: 10px 0;
        }

        /* ============================================================
           ПОДВАЛ С ЛОГОТИПОМ
           ============================================================ */
        footer {
            margin-top: 30px;
            padding: 20px 0;
            border-top: 1px solid #1a2a40;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        footer .footer-logo {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9em;
            color: #5a6a8a;
        }

        footer .footer-logo svg {
            width: 30px;
            height: 30px;
        }

        footer .footer-logo span {
            color: #7b2ffc;
        }

        footer .footer-text {
            color: #3a4a5a;
            font-size: 0.8em;
        }

        footer .footer-text span {
            color: #7b2ffc;
        }

        /* ============================================================
           СКРОЛЛ
           ============================================================ */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0e17;
        }
        ::-webkit-scrollbar-thumb {
            background: #2a3a5a;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #3a4a6a;
        }

        /* ============================================================
           АДАПТИВ
           ============================================================ */
        @media (max-width: 600px) {
            body {
                padding: 10px;
            }
            .doc-grid {
                grid-template-columns: 1fr;
            }
            .tabs {
                flex-wrap: wrap;
            }
            .tab-btn {
                padding: 8px 16px;
                font-size: 0.85em;
            }
            .toolbar .btn {
                font-size: 0.85em;
                padding: 8px 16px;
            }
            header {
                flex-direction: column;
                align-items: stretch;
                padding: 15px;
            }
            .header-right {
                justify-content: space-between;
            }
            .logo-text {
                font-size: 1.1em;
            }
            .logo svg {
                width: 40px;
                height: 40px;
            }
            footer {
                flex-direction: column;
                text-align: center;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- ============================================================
        ШАПКА С ВСТРОЕННЫМ ЛОГОТИПОМ (НЕУБИРАЕМЫЙ)
        ============================================================ -->
        <header>
            <div class="logo">
                <!-- ============================================================
                ОСНОВНОЙ ЛОГОТИП ТРИТОНА — ВСТРОЕН НАВСЕГДА!
                ============================================================ -->
                <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                    <!-- Фон -->
                    <circle cx="100" cy="100" r="90" fill="#0a0e17" stroke="#7b2ffc" stroke-width="4"/>

                    <!-- Буква Т (волна) -->
                    <path d="M 50 40 L 150 40 L 150 65 L 110 65 L 110 160 L 90 160 L 90 65 L 50 65 Z"
                          fill="#00d4ff" opacity="0.9"/>

                    <!-- Вторичная волна -->
                    <path d="M 60 85 Q 100 70 140 85 Q 160 95 170 85"
                          stroke="#7b2ffc" stroke-width="3" fill="none"/>

                    <!-- Атомы/круги -->
                    <circle cx="60" cy="130" r="12" fill="#7b2ffc" opacity="0.6"/>
                    <circle cx="100" cy="150" r="10" fill="#00d4ff" opacity="0.6"/>
                    <circle cx="140" cy="130" r="12" fill="#7b2ffc" opacity="0.6"/>

                    <!-- Название -->
                    <text x="100" y="185" text-anchor="middle" fill="#c8d0e0"
                          font-family="Arial" font-size="18" font-weight="bold">ТРИТОН</text>
                </svg>

                <span class="logo-text">Тритон</span>
                <span class="logo-badge">✅ РАБОТАЕТ!</span>
            </div>

            <div class="header-right">
                <span class="info">⚡ <span>100+</span> команд</span>
                <span class="info">📚 Встроенная справка</span>
            </div>
        </header>

        <!-- ============================================================
        ВКЛАДКИ
        ============================================================ -->
        <div class="tabs">
            <button class="tab-btn active" data-tab="editor">📝 Редактор</button>
            <button class="tab-btn" data-tab="docs">📚 Справка (100+ команд)</button>
        </div>

        <!-- ============================================================
        ВКЛАДКА: РЕДАКТОР
        ============================================================ -->
        <div class="tab-content active" id="tab-editor">
            <div class="toolbar">
                <button class="btn btn-run" onclick="runCode()">▶ Запустить</button>
                <button class="btn btn-clear" onclick="clearOutput()">🗑 Очистить</button>
                <button class="btn btn-save" onclick="saveCode()">💾 Сохранить</button>
                <button class="btn btn-load" onclick="loadCode()">📂 Загрузить</button>
                <span style="color:#5a6a8a; font-size:0.85em; display:flex; align-items:center; margin-left:auto;">
                    Ctrl+Enter для запуска
                </span>
            </div>

            <div class="main-grid">
                <div class="panel">
                    <div class="panel-label">
                        <span>📝 Код на Тритоне</span>
                        <span class="badge" style="background:#1a2a40;color:#7b8baa;border:none;">.тритон</span>
                    </div>
                    <textarea id="code" spellcheck="false">// Первая программа на Тритоне
скажи("Привет, мир!")

имя = "Алексей"
возраст = 30

скажи("Меня зовут " + имя)
скажи("Через 5 лет мне будет " + (возраст + 5))

если возраст > 18 то
    скажи("Ты взрослый!")
иначе
    скажи("Ты ещё ребёнок!")
конец

// Цикл
счет = 0
пока счет < 3 то
    скажи("Счёт: " + счет)
    счет = счет + 1
конец

// Список
дела = ["Учеба", "Еда", "Сон"]
для дело из дела то
    скажи("Дело: " + дело)
конец</textarea>
                </div>

                <div class="panel">
                    <div class="panel-label">
                        <span>📤 Вывод</span>
                        <span class="badge" id="statusBadge" style="background:#1a2a40;color:#7b8baa;border:none;">готов</span>
                    </div>
                    <div class="output" id="output"></div>
                </div>
            </div>

            <div class="status-bar">
                <span>🐚 Тритон v1.0 • Работает в браузере</span>
                <span id="timeInfo">⏱ 0ms</span>
            </div>
        </div>

        <!-- ============================================================
        ВКЛАДКА: СПРАВКА
        ============================================================ -->
        <div class="tab-content" id="tab-docs">
            <div class="doc-search">
                <input type="text" id="docSearch" placeholder="🔍 Поиск по командам..." oninput="searchDocs()">
                <span class="doc-count" id="docCount">Всего команд: 0</span>
            </div>
            <div class="doc-grid" id="docGrid"></div>
        </div>

        <!-- ============================================================
        ПОДВАЛ С ЛОГОТИПОМ (НЕУБИРАЕМЫЙ)
        ============================================================ -->
        <footer>
            <div class="footer-logo">
                <!-- Маленький логотип в подвале -->
                <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" width="30" height="30">
                    <circle cx="100" cy="100" r="90" fill="#0a0e17" stroke="#7b2ffc" stroke-width="4"/>
                    <path d="M 50 40 L 150 40 L 150 65 L 110 65 L 110 160 L 90 160 L 90 65 L 50 65 Z" fill="#00d4ff" opacity="0.9"/>
                    <circle cx="60" cy="130" r="12" fill="#7b2ffc" opacity="0.6"/>
                    <circle cx="100" cy="150" r="10" fill="#00d4ff" opacity="0.6"/>
                    <circle cx="140" cy="130" r="12" fill="#7b2ffc" opacity="0.6"/>
                </svg>
                <span>© 2026 <span>Тритон</span> — русский язык программирования</span>
            </div>
            <div class="footer-text">
                <span>🐚</span> Сделано с ❤️ к русскому языку • Свободное ПО
            </div>
        </footer>
    </div>

    <script>
        // ================================================================
        // 100+ КОМАНД ДЛЯ СПРАВКИ
        // ================================================================

        const commands = [
            // ---- ОСНОВНЫЕ ----
            { cmd: 'скажи(выражение)', desc: 'Выводит текст или значение на экран.', example: 'скажи("Привет, мир!")',
                tags: ['вывод'] },
            { cmd: 'спроси переменная', desc: 'Запрашивает ввод от пользователя и сохраняет в переменную.',
                example: 'спроси возраст', tags: ['ввод'] },
            { cmd: 'остановить', desc: 'Немедленно завершает программу.', example: 'остановить', tags: ['управление'] },
            { cmd: 'подождать(мс)', desc: 'Приостанавливает программу на указанное количество миллисекунд.',
                example: 'подождать(2000)', tags: ['таймер'] },
            { cmd: 'очистить', desc: 'Очищает экран консоли.', example: 'очистить', tags: ['консоль'] },

            // ---- ПЕРЕМЕННЫЕ ----
            { cmd: 'переменная = значение', desc: 'Создаёт переменную и присваивает ей значение.',
                example: 'имя = "Анна"\nвозраст = 25', tags: ['переменные'] },
            { cmd: 'тип(переменная)', desc: 'Возвращает тип переменной: число, строка, логий, список.',
                example: 'скажи(тип(42))  // число', tags: ['типы'] },
            { cmd: 'существует(переменная)', desc: 'Проверяет, существует ли переменная. Возвращает истина/ложь.',
                example: 'если существует(имя) то...', tags: ['проверка'] },
            { cmd: 'удалить(переменная)', desc: 'Удаляет переменную из памяти.', example: 'удалить(временная)',
                tags: ['память'] },
            { cmd: 'константа имя = значение', desc: 'Создаёт неизменяемую константу.',
                example: 'константа ПИ = 3.14159', tags: ['константы'] },
            { cmd: 'скопировать(переменная)', desc: 'Создаёт глубокую копию переменной (для списков).',
                example: 'копия = скопировать(список)', tags: ['копирование'] },

            // ---- УСЛОВИЯ ----
            { cmd: 'если условие то ... иначе ... конец', desc: 'Условный оператор. Выполняет блок, если условие истинно.',
                example: 'если возраст > 18 то\n    скажи("Взрослый")\nиначе\n    скажи("Ребёнок")\nконец',
                tags: ['условия'] },
            { cmd: 'иначе_если условие то', desc: 'Дополнительное условие после "если".',
                example: 'если x > 90 то ...\nиначе_если x > 70 то ...', tags: ['условия'] },
            { cmd: 'выбор переменная ... вариант ... иначе ... конец', desc: 'Множественный выбор (как switch).',
                example: 'выбор день\n    вариант "Пн": скажи("Понедельник")\n    иначе: скажи("Другой день")\nконец',
                tags: ['условия'] },
            { cmd: 'и, или, не', desc: 'Логические операторы для сложных условий.',
                example: 'если (a > 5) и (b < 10) то...', tags: ['логика'] },

            // ---- ЦИКЛЫ ----
            { cmd: 'пока условие то ... конец', desc: 'Цикл с предусловием. Выполняется, пока условие истинно.',
                example: 'пока счет < 5 то\n    скажи(счет)\n    счет = счет + 1\nконец', tags: ['циклы'] },
            { cmd: 'для переменная из список то ... конец', desc: 'Цикл по элементам списка.',
                example: 'для город из ["Мск","Пб"] то\n    скажи(город)\nконец', tags: ['циклы'] },
            { cmd: 'повторить(число) ... конец', desc: 'Выполняет блок кода указанное количество раз.',
                example: 'повторить(5)\n    скажи("Привет!")\nконец', tags: ['циклы'] },
            { cmd: 'прервать', desc: 'Немедленно выходит из цикла.', example: 'если x == 0 то прервать конец',
                tags: ['циклы'] },
            { cmd: 'продолжить', desc: 'Переходит к следующей итерации цикла.', example: 'если x % 2 == 0 то продолжить конец',
                tags: ['циклы'] },

            // ---- ФУНКЦИИ ----
            { cmd: 'функция имя(арг) ... вернуть ... конец', desc: 'Объявляет функцию с аргументами.',
                example: 'функция сумма(a, b)\n    вернуть a + b\nконец', tags: ['функции'] },
            { cmd: 'вернуть значение', desc: 'Возвращает значение из функции и завершает её.',
                example: 'вернуть x * x', tags: ['функции'] },
            { cmd: 'функция(арг = значение)', desc: 'Аргументы со значениями по умолчанию.',
                example: 'функция привет(имя = "Мир")\n    скажи("Привет, " + имя)\nконец', tags: ['функции'] },

            // ---- СПИСКИ ----
            { cmd: '[элемент1, элемент2, ...]', desc: 'Список (массив) — набор значений.',
                example: 'числа = [1, 2, 3, 4, 5]', tags: ['списки'] },
            { cmd: 'список[индекс]', desc: 'Обращение к элементу списка по индексу (с 0).',
                example: 'первый = числа[0]', tags: ['списки'] },
            { cmd: 'добавить(список, элемент)', desc: 'Добавляет элемент в конец списка.',
                example: 'добавить(дела, "Новое дело")', tags: ['списки'] },
            { cmd: 'вставить(список, индекс, элемент)', desc: 'Вставляет элемент в список по индексу.',
                example: 'вставить(дела, 0, "Важное")', tags: ['списки'] },
            { cmd: 'удалить_из(список, индекс)', desc: 'Удаляет элемент из списка по индексу.',
                example: 'удалить_из(дела, 2)', tags: ['списки'] },
            { cmd: 'длина(список)', desc: 'Возвращает длину списка или строки.', example: 'скажи(длина(дела))',
                tags: ['списки'] },
            { cmd: 'содержит(список, элемент)', desc: 'Проверяет, содержит ли список элемент.',
                example: 'если содержит(числа, 5) то...', tags: ['списки'] },
            { cmd: 'срез(список, от, до)', desc: 'Возвращает часть списка (как срез).',
                example: 'первые_три = срез(числа, 0, 3)', tags: ['списки'] },

            // ---- СТРОКИ ----
            { cmd: '"текст" или \'текст\'', desc: 'Строковый литерал.', example: 'имя = "Анна"',
            tags: ['строки'] },
            { cmd: 'строка + строка', desc: 'Объединение строк (конкатенация).',
                example: 'привет = "Привет, " + имя', tags: ['строки'] },
            { cmd: 'верх(строка)', desc: 'Преобразует строку в верхний регистр.', example: 'скажи(верх("привет"))',
                tags: ['строки'] },
            { cmd: 'низ(строка)', desc: 'Преобразует строку в нижний регистр.', example: 'скажи(низ("ПРИВЕТ"))',
                tags: ['строки'] },
            { cmd: 'заменить(строка, что, на_что)', desc: 'Заменяет подстроку в строке.',
                example: 'новая = заменить(текст, "мир", "все")', tags: ['строки'] },
            { cmd: 'разделить(строка, разделитель)', desc: 'Разбивает строку на список по разделителю.',
                example: 'слова = разделить("раз-два-три", "-")', tags: ['строки'] },
            { cmd: 'объединить(список, разделитель)', desc: 'Объединяет список строк в одну строку с разделителем.',
                example: 'текст = объединить(слова, " ")', tags: ['строки'] },
            { cmd: 'подстрока(строка, от, до)', desc: 'Извлекает подстроку из строки.',
                example: 'часть = подстрока("Привет", 0, 3)  // "При"', tags: ['строки'] },

            // ---- МАТЕМАТИКА ----
            { cmd: 'число + число', desc: 'Сложение чисел.', example: 'сумма = 10 + 20', tags: ['математика'] },
            { cmd: 'число - число', desc: 'Вычитание чисел.', example: 'разность = 20 - 10', tags: ['математика'] },
            { cmd: 'число * число', desc: 'Умножение чисел.', example: 'произведение = 5 * 6', tags: ['математика'] },
            { cmd: 'число / число', desc: 'Деление чисел.', example: 'частное = 10 / 2', tags: ['математика'] },
            { cmd: 'число % число', desc: 'Остаток от деления (модуль).', example: 'остаток = 10 % 3  // 1',
                tags: ['математика'] },
            { cmd: 'число ** число', desc: 'Возведение в степень.', example: 'квадрат = 5 ** 2  // 25',
                tags: ['математика'] },
            { cmd: 'abs(число)', desc: 'Модуль числа (абсолютное значение).', example: 'скажи(abs(-10))  // 10',
                tags: ['математика'] },
            { cmd: 'округлить(число)', desc: 'Округляет число до ближайшего целого.',
                example: 'скажи(округлить(3.7))  // 4', tags: ['математика'] },
            { cmd: 'случайное(мин, макс)', desc: 'Генерирует случайное число в диапазоне.',
                example: 'число = случайное(1, 100)', tags: ['математика'] },
            { cmd: 'случайный_выбор(список)', desc: 'Выбирает случайный элемент из списка.',
                example: 'выбор = случайный_выбор(["A","B","C"])', tags: ['математика'] },

            // ---- ФАЙЛЫ ----
            { cmd: 'открыть(путь, режим)', desc: 'Открывает файл для чтения или записи.',
                example: 'открыть("file.txt", "чтение")', tags: ['файлы'] },
            { cmd: 'закрыть()', desc: 'Закрывает текущий файл.', example: 'закрыть()', tags: ['файлы'] },
            { cmd: 'прочитать()', desc: 'Читает содержимое файла в строку.', example: 'текст = прочитать()',
                tags: ['файлы'] },
            { cmd: 'прочитать_строки()', desc: 'Читает файл по строкам в список.', example: 'строки = прочитать_строки()',
                tags: ['файлы'] },
            { cmd: 'записать(текст)', desc: 'Записывает текст в файл.', example: 'записать("Новая строка")',
                tags: ['файлы'] },
            { cmd: 'дописать(текст)', desc: 'Добавляет текст в конец файла.', example: 'дописать("Ещё строка")',
                tags: ['файлы'] },
            { cmd: 'существует_файл(путь)', desc: 'Проверяет, существует ли файл.', example: 'если существует_файл("data.txt") то...',
                tags: ['файлы'] },
            { cmd: 'удалить_файл(путь)', desc: 'Удаляет файл.', example: 'удалить_файл("temp.txt")',
            tags: ['файлы'] },

            // ---- ДАТА И ВРЕМЯ ----
            { cmd: 'сейчас()', desc: 'Возвращает текущую дату и время.', example: 'теперь = сейчас()',
                tags: ['дата'] },
            { cmd: 'год(дата)', desc: 'Возвращает год из даты.', example: 'год_сейчас = год(сейчас())',
                tags: ['дата'] },
            { cmd: 'месяц(дата)', desc: 'Возвращает месяц из даты (1-12).', example: 'месяц_сейчас = месяц(сейчас())',
                tags: ['дата'] },
            { cmd: 'день(дата)', desc: 'Возвращает день из даты (1-31).', example: 'день_сейчас = день(сейчас())',
                tags: ['дата'] },
            { cmd: 'часы(дата)', desc: 'Возвращает часы из времени (0-23).', example: 'час = часы(сейчас())',
                tags: ['дата'] },
            { cmd: 'минуты(дата)', desc: 'Возвращает минуты из времени (0-59).', example: 'мин = минуты(сейчас())',
                tags: ['дата'] },
            { cmd: 'секунды(дата)', desc: 'Возвращает секунды из времени (0-59).', example: 'сек = секунды(сейчас())',
                tags: ['дата'] },
            { cmd: 'день_недели(дата)', desc: 'Возвращает день недели (1-7, 1=пн).', example: 'день = день_недели(сейчас())',
                tags: ['дата'] },
            { cmd: 'формат_даты(дата, формат)', desc: 'Форматирует дату по шаблону.',
                example: 'скажи(формат_даты(сейчас(), "DD.MM.YYYY"))', tags: ['дата'] },

            // ---- HTTP / ИНТЕРНЕТ ----
            { cmd: 'запросить(метод, url)', desc: 'Выполняет HTTP-запрос и возвращает ответ.',
                example: 'ответ = запросить("GET", "https://api.example.com")', tags: ['интернет'] },
            { cmd: 'ответ.статус', desc: 'Код статуса HTTP-ответа.', example: 'скажи(ответ.статус)  // 200',
                tags: ['интернет'] },
            { cmd: 'ответ.текст', desc: 'Тело ответа как текст.', example: 'скажи(ответ.текст)', tags: ['интернет'] },
            { cmd: 'ответ.json', desc: 'Разбирает ответ как JSON.', example: 'данные = ответ.json', tags: ['интернет'] },
            { cmd: 'отправить_данные(url, данные)', desc: 'Отправляет данные POST-запросом.',
                example: 'отправить_данные("https://api.com", {"имя": "Анна"})', tags: ['интернет'] },

            // ---- СИСТЕМНЫЕ ----
            { cmd: 'команда(строка)', desc: 'Выполняет системную команду в терминале.',
                example: 'команда("ls -la")', tags: ['система'] },
            { cmd: 'переменная_окружения(имя)', desc: 'Получает значение переменной окружения.',
                example: 'путь = переменная_окружения("PATH")', tags: ['система'] },
            { cmd: 'текущая_папка()', desc: 'Возвращает путь к текущей рабочей папке.',
                example: 'папка = текущая_папка()', tags: ['система'] },
            { cmd: 'сменить_папку(путь)', desc: 'Меняет текущую рабочую папку.',
                example: 'сменить_папку("/home/user")', tags: ['система'] },
            { cmd: 'список_файлов(путь)', desc: 'Возвращает список файлов в папке.',
                example: 'файлы = список_файлов(".")', tags: ['система'] },

            // ---- ГРАФИКА ----
            { cmd: 'цвет(цвет)', desc: 'Меняет цвет вывода в консоли.',
                example: 'цвет("красный")\nскажи("Красный текст")', tags: ['графика'] },
            { cmd: 'цвет_фона(цвет)', desc: 'Меняет цвет фона в консоли.', example: 'цвет_фона("синий")',
                tags: ['графика'] },
            { cmd: 'скинуть_цвет()', desc: 'Сбрасывает цвета к стандартным.', example: 'скинуть_цвет()',
                tags: ['графика'] },
            { cmd: 'прогресс(текущий, максимум)', desc: 'Показывает прогресс-бар в консоли.',
                example: 'прогресс(50, 100)', tags: ['графика'] },

            // ---- ОШИБКИ ----
            { cmd: 'попробовать ... поймать ... конец', desc: 'Обработка ошибок (try-catch).',
                example: 'попробовать\n    результат = 10 / 0\nпоймать\n    скажи("Ошибка деления!")\nконец',
                tags: ['ошибки'] },
            { cmd: 'вызвать_ошибку(текст)', desc: 'Генерирует ошибку с указанным текстом.',
                example: 'вызвать_ошибку("Что-то пошло не так")', tags: ['ошибки'] },
            { cmd: 'тип_ошибки(ошибка)', desc: 'Возвращает тип ошибки.', example: 'скажи(тип_ошибки(ошибка))',
                tags: ['ошибки'] },
            { cmd: 'отладка(значение)', desc: 'Выводит отладочную информацию с именем переменной.',
                example: 'отладка(х)', tags: ['отладка'] },

            // ---- ДОПОЛНИТЕЛЬНЫЕ ----
            { cmd: 'ждать_нажатие()', desc: 'Ожидает нажатия любой клавиши пользователем.',
                example: 'ждать_нажатие()', tags: ['ввод'] },
            { cmd: 'время_выполнения(функция)', desc: 'Замеряет время выполнения функции в миллисекундах.',
                example: 'время = время_выполнения(моя_функция)', tags: ['таймер'] },
            { cmd: 'проверить_тип(значение, тип)', desc: 'Проверяет, соответствует ли значение типу.',
                example: 'если проверить_тип(х, "число") то...', tags: ['типы'] },
            { cmd: 'преобразовать_в_число(строка)', desc: 'Преобразует строку в число.',
                example: 'число = преобразовать_в_число("42")', tags: ['преобразование'] },
            { cmd: 'преобразовать_в_строку(значение)', desc: 'Преобразует значение в строку.',
                example: 'текст = преобразовать_в_строку(123)', tags: ['преобразование'] },
            { cmd: 'рандомное_имя()', desc: 'Генерирует случайное имя для файлов или переменных.',
                example: 'имя_файла = рандомное_имя()', tags: ['случайные'] },
            { cmd: 'сортировать(список)', desc: 'Сортирует список в порядке возрастания.',
                example: 'сортировать(числа)', tags: ['списки'] },
            { cmd: 'сортировать_по(список, ключ)', desc: 'Сортирует список по ключу.',
                example: 'сортировать_по(пользователи, "возраст")', tags: ['списки'] },
            { cmd: 'перевернуть(список)', desc: 'Переворачивает список (реверс).',
                example: 'перевернуть(числа)', tags: ['списки'] },
            { cmd: 'сумма(список)', desc: 'Возвращает сумму всех чисел в списке.',
                example: 'сумма_всех = сумма(числа)', tags: ['математика'] },
            { cmd: 'среднее(список)', desc: 'Возвращает среднее арифметическое чисел в списке.',
                example: 'среднее_знач = среднее(числа)', tags: ['математика'] },
            { cmd: 'максимум(список)', desc: 'Возвращает максимальное значение в списке.',
                example: 'макс = максимум(числа)', tags: ['математика'] },
            { cmd: 'минимум(список)', desc: 'Возвращает минимальное значение в списке.',
                example: 'мин = минимум(числа)', tags: ['математика'] },
            { cmd: 'степень(число, степень)', desc: 'Возводит число в указанную степень.',
                example: 'квадрат = степень(5, 2)  // 25', tags: ['математика'] },
            { cmd: 'корень(число)', desc: 'Извлекает квадратный корень из числа.',
                example: 'корень_из_16 = корень(16)  // 4', tags: ['математика'] },
            { cmd: 'логарифм(число)', desc: 'Вычисляет натуральный логарифм числа.',
                example: 'лн = логарифм(10)', tags: ['математика'] },
            { cmd: 'синус(угол)', desc: 'Вычисляет синус угла в радианах.', example: 'син = синус(1.57)',
                tags: ['математика'] },
            { cmd: 'косинус(угол)', desc: 'Вычисляет косинус угла в радианах.', example: 'кос = косинус(0)',
                tags: ['математика'] },
            { cmd: 'тангенс(угол)', desc: 'Вычисляет тангенс угла в радианах.', example: 'танг = тангенс(0.785)',
                tags: ['математика'] },
            { cmd: 'экспонента(число)', desc: 'Вычисляет экспоненту числа (e^x).',
                example: 'exp = экспонента(1)  // 2.718', tags: ['математика'] },
            { cmd: 'факториал(число)', desc: 'Вычисляет факториал числа.', example: 'факт = факториал(5)  // 120',
                tags: ['математика'] },
            { cmd: 'дробная_часть(число)', desc: 'Возвращает дробную часть числа.',
                example: 'дробь = дробная_часть(3.14)  // 0.14', tags: ['математика'] },
            { cmd: 'целая_часть(число)', desc: 'Возвращает целую часть числа.',
                example: 'целое = целая_часть(3.14)  // 3', tags: ['математика'] },

            // ---- JSON ----
            { cmd: 'json_парсить(строка)', desc: 'Преобразует строку JSON в объект.',
                example: 'данные = json_парсить(\'{"имя":"Анна"}\')', tags: ['json'] },
            { cmd: 'json_строка(объект)', desc: 'Преобразует объект в строку JSON.',
                example: 'текст = json_строка(данные)', tags: ['json'] },

            // ---- КОНСОЛЬ ----
            { cmd: 'цвет_текста(цвет)', desc: 'Устанавливает цвет текста в консоли.',
                example: 'цвет_текста("зелёный")', tags: ['консоль'] },
            { cmd: 'цвет_фона(цвет)', desc: 'Устанавливает цвет фона в консоли.',
                example: 'цвет_фона("чёрный")', tags: ['консоль'] },
            { cmd: 'сбросить_цвета()', desc: 'Сбрасывает цвета консоли к стандартным.',
                example: 'сбросить_цвета()', tags: ['консоль'] },

            // ---- ДОПОЛНИТЕЛЬНО ----
            { cmd: 'задержка(мс)', desc: 'То же что и подождать().', example: 'задержка(1000)', tags: ['таймер'] },
            { cmd: 'пауза(мс)', desc: 'То же что и подождать().', example: 'пауза(500)', tags: ['таймер'] },
            { cmd: 'вывод(текст)', desc: 'То же что и скажи().', example: 'вывод("Привет")', tags: ['вывод'] },
            { cmd: 'печать(текст)', desc: 'То же что и скажи().', example: 'печать("Привет")', tags: ['вывод'] },
            { cmd: 'показать(текст)', desc: 'То же что и скажи().', example: 'показать("Привет")', tags: ['вывод'] },
        ];

        // ================================================================
        // РАБОЧИЙ ИНТЕРПРЕТАТОР ТРИТОНА
        // ================================================================

        function runCode() {
            const code = document.getElementById('code').value;
            const output = document.getElementById('output');
            const status = document.getElementById('statusBadge');
            const timeInfo = document.getElementById('timeInfo');

            output.innerHTML = '';
            status.textContent = '⏳ выполняется...';
            status.style.color = '#ffd93d';

            const start = performance.now();

            const variables = {};
            const functions = {};
            let outputText = [];

            function log(msg, type = 'log') {
                outputText.push(msg);
                const div = document.createElement('div');
                div.className = type;
                div.textContent = '> ' + msg;
                output.appendChild(div);
            }

            function getValue(expr) {
                expr = expr.trim();

                if (!expr) return '';

                if ((expr.startsWith('"') && expr.endsWith('"')) ||
                    (expr.startsWith("'") && expr.endsWith("'"))) {
                    return expr.slice(1, -1);
                }

                if (/^-?\d+(\.\d+)?$/.test(expr)) {
                    return parseFloat(expr);
                }

                if (expr === 'истина') return true;
                if (expr === 'ложь') return false;

                if (expr.startsWith('[') && expr.endsWith(']')) {
                    const content = expr.slice(1, -1).trim();
                    if (!content) return [];
                    const items = [];
                    let current = '';
                    let brackets = 0;
                    let inString = false;
                    let quote = '';

                    for (const char of content) {
                        if ((char === '"' || char === "'") && (brackets === 0 || inString)) {
                            if (inString && char === quote) {
                                inString = false;
                            } else if (!inString) {
                                inString = true;
                                quote = char;
                            }
                            current += char;
                            continue;
                        }
                        if (char === '[' && !inString) brackets++;
                        if (char === ']' && !inString) brackets--;
                        if (char === ',' && brackets === 0 && !inString) {
                            items.push(getValue(current.trim()));
                            current = '';
                            continue;
                        }
                        current += char;
                    }
                    if (current.trim()) {
                        items.push(getValue(current.trim()));
                    }
                    return items;
                }

                const funcMatch = expr.match(/^(\w+)\s*\(([^)]*)\)$/);
                if (funcMatch) {
                    const name = funcMatch[1];
                    const argsStr = funcMatch[2].trim();
                    const args = argsStr ? argsStr.split(',').map(s => getValue(s.trim())) : [];

                    // Встроенные функции (сокращённо)
                    const builtins = {
                        'длина': (a) => Array.isArray(a) ? a.length : (typeof a === 'string' ? a.length : 0),
                        'добавить': (a, b) => { if (Array.isArray(a)) { a.push(b); return a; } return a; },
                        'вставить': (a, b, c) => { if (Array.isArray(a)) { a.splice(b, 0, c); return a; } return a; },
                        'удалить_из': (a, b) => { if (Array.isArray(a)) { a.splice(b, 1); return a; } return a; },
                        'содержит': (a, b) => Array.isArray(a) ? a.includes(b) : false,
                        'срез': (a, b, c) => Array.isArray(a) ? a.slice(b, c) : a,
                        'верх': (a) => String(a).toUpperCase(),
                        'низ': (a) => String(a).toLowerCase(),
                        'заменить': (a, b, c) => String(a).replaceAll(b, c),
                        'разделить': (a, b) => String(a).split(b),
                        'объединить': (a, b) => Array.isArray(a) ? a.join(b || '') : a,
                        'подстрока': (a, b, c) => String(a).substring(b, c),
                        'abs': (a) => Math.abs(a),
                        'округлить': (a) => Math.round(a),
                        'случайное': (a, b) => Math.floor(Math.random() * (b - a + 1)) + a,
                        'случайный_выбор': (a) => Array.isArray(a) ? a[Math.floor(Math.random() * a.length)] : a,
                        'сейчас': () => new Date().toString(),
                        'год': (a) => new Date(a).getFullYear(),
                        'месяц': (a) => new Date(a).getMonth() + 1,
                        'день': (a) => new Date(a).getDate(),
                        'часы': (a) => new Date(a).getHours(),
                        'минуты': (a) => new Date(a).getMinutes(),
                        'секунды': (a) => new Date(a).getSeconds(),
                        'день_недели': (a) => new Date(a).getDay() || 7,
                        'формат_даты': (a, b) => {
                            const d = new Date(a);
                            const fmt = b || 'DD.MM.YYYY';
                            return fmt.replace('YYYY', d.getFullYear())
                                .replace('MM', String(d.getMonth() + 1).padStart(2, '0'))
                                .replace('DD', String(d.getDate()).padStart(2, '0'))
                                .replace('HH', String(d.getHours()).padStart(2, '0'))
                                .replace('mm', String(d.getMinutes()).padStart(2, '0'))
                                .replace('SS', String(d.getSeconds()).padStart(2, '0'));
                        },
                        'тип': (a) => Array.isArray(a) ? 'список' : typeof a,
                        'существует': (a) => a in variables,
                        'удалить': (a) => { delete variables[a]; return true; },
                        'скопировать': (a) => Array.isArray(a) ? [...a] : (typeof a === 'object' ? { ...a } : a),
                        'сумма': (a) => Array.isArray(a) ? a.reduce((x, y) => x + y, 0) : a,
                        'среднее': (a) => Array.isArray(a) ? a.reduce((x, y) => x + y, 0) / a.length : a,
                        'максимум': (a) => Array.isArray(a) ? Math.max(...a) : a,
                        'минимум': (a) => Array.isArray(a) ? Math.min(...a) : a,
                        'степень': (a, b) => Math.pow(a, b),
                        'корень': (a) => Math.sqrt(a),
                        'логарифм': (a) => Math.log(a),
                        'синус': (a) => Math.sin(a),
                        'косинус': (a) => Math.cos(a),
                        'тангенс': (a) => Math.tan(a),
                        'экспонента': (a) => Math.exp(a),
                        'факториал': (a) => { let r = 1; for (let i = 2; i <= a; i++) r *= i; return r; },
                        'дробная_часть': (a) => a - Math.floor(a),
                        'целая_часть': (a) => Math.floor(a),
                        'json_парсить': (a) => { try { return JSON.parse(a); } catch (e) { return null; } },
                        'json_строка': (a) => { try { return JSON.stringify(a); } catch (e) { return null; } },
                        'сортировать': (a) => Array.isArray(a) ? [...a].sort() : a,
                        'сортировать_по': (a, b) => {
                            if (Array.isArray(a)) {
                                return [...a].sort((x, y) => {
                                    const key = b;
                                    if (typeof x === 'object' && typeof y === 'object') {
                                        return x[key] > y[key] ? 1 : -1;
                                    }
                                    return x > y ? 1 : -1;
                                });
                            }
                            return a;
                        },
                        'перевернуть': (a) => Array.isArray(a) ? [...a].reverse() : a,
                    };

                    if (name in builtins) {
                        return builtins[name](...args);
                    }

                    if (functions[name]) {
                        const func = functions[name];
                        const oldVars = { ...variables };
                        for (let i = 0; i < func.args.length && i < args.length; i++) {
                            variables[func.args[i]] = args[i];
                        }
                        let result = null;
                        let returned = false;
                        let k = 0;
                        while (k < func.body.length && !returned) {
                            const line = func.body[k].trim();
                            if (line.startsWith('вернуть')) {
                                const m = line.match(/вернуть\s+(.+)/);
                                if (m) {
                                    result = getValue(m[1].trim());
                                    returned = true;
                                }
                            } else {
                                if (line.includes('=') && !line.startsWith('если')) {
                                    const parts = line.split('=');
                                    variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                } else if (line.startsWith('скажи')) {
                                    const m = line.match(/скажи\((.*)\)/);
                                    if (m) log(String(getValue(m[1].trim())));
                                }
                            }
                            k++;
                        }
                        Object.assign(variables, oldVars);
                        return result !== null ? result : '';
                    }

                    return expr;
                }

                let processed = expr;

                while (processed.includes('(')) {
                    const open = processed.lastIndexOf('(');
                    const close = processed.indexOf(')', open);
                    if (close === -1) break;
                    const inner = processed.slice(open + 1, close);
                    const value = getValue(inner);
                    processed = processed.slice(0, open) + String(value) + processed.slice(close + 1);
                }

                let parts = splitByOps(processed, ['*', '/']);
                if (parts.length > 1) {
                    let result = getValue(parts[0].trim());
                    for (let i = 1; i < parts.length; i += 2) {
                        const op = parts[i];
                        const right = getValue(parts[i + 1].trim());
                        if (op === '*') result *= right;
                        else if (op === '/') {
                            if (right === 0) {
                                log('❌ Деление на ноль!', 'error');
                                return 0;
                            }
                            result /= right;
                        }
                    }
                    return result;
                }

                parts = splitByOps(processed, ['+', '-']);
                if (parts.length > 1) {
                    let result = getValue(parts[0].trim());
                    for (let i = 1; i < parts.length; i += 2) {
                        const op = parts[i];
                        const right = getValue(parts[i + 1].trim());
                        if (op === '+') {
                            if (typeof result === 'string' || typeof right === 'string') {
                                result = String(result) + String(right);
                            } else {
                                result += right;
                            }
                        } else if (op === '-') {
                            result -= right;
                        }
                    }
                    return result;
                }

                if (processed.includes('==')) {
                    const [l, r] = processed.split('==');
                    return getValue(l.trim()) == getValue(r.trim());
                }
                if (processed.includes('!=')) {
                    const [l, r] = processed.split('!=');
                    return getValue(l.trim()) != getValue(r.trim());
                }
                if (processed.includes('>=')) {
                    const [l, r] = processed.split('>=');
                    return getValue(l.trim()) >= getValue(r.trim());
                }
                if (processed.includes('<=')) {
                    const [l, r] = processed.split('<=');
                    return getValue(l.trim()) <= getValue(r.trim());
                }
                if (processed.includes('>')) {
                    const [l, r] = processed.split('>');
                    return getValue(l.trim()) > getValue(r.trim());
                }
                if (processed.includes('<')) {
                    const [l, r] = processed.split('<');
                    return getValue(l.trim()) < getValue(r.trim());
                }

                if (processed in variables) {
                    return variables[processed];
                }

                return processed;
            }

            function splitByOps(str, ops) {
                const result = [];
                let current = '';
                let brackets = 0;
                let inString = false;
                let quote = '';

                for (const char of str) {
                    if ((char === '"' || char === "'") && (brackets === 0 || inString)) {
                        if (inString && char === quote) {
                            inString = false;
                        } else if (!inString) {
                            inString = true;
                            quote = char;
                        }
                        current += char;
                        continue;
                    }
                    if (char === '(' && !inString) brackets++;
                    if (char === ')' && !inString) brackets--;
                    if (brackets === 0 && !inString && ops.includes(char)) {
                        if (current.trim()) {
                            result.push(current.trim());
                        }
                        result.push(char);
                        current = '';
                        continue;
                    }
                    current += char;
                }
                if (current.trim()) {
                    result.push(current.trim());
                }
                return result;
            }

            function execute(lines, startIdx) {
                let i = startIdx;
                while (i < lines.length) {
                    const line = lines[i].trim();
                    i++;

                    if (!line || line.startsWith('//') || line.startsWith('#')) continue;

                    if (line.startsWith('скажи') || line.startsWith('вывод') ||
                        line.startsWith('печать') || line.startsWith('показать')) {
                        const match = line.match(/(скажи|вывод|печать|показать)\((.*)\)/);
                        if (match) {
                            const val = getValue(match[2].trim());
                            log(String(val));
                        }
                        continue;
                    }

                    if (line.startsWith('спроси')) {
                        const match = line.match(/спроси\s+(\w+)/);
                        if (match) {
                            const val = prompt('Введите значение для "' + match[1] + '":');
                            variables[match[1]] = val !== null ? val : '';
                        }
                        continue;
                    }

                    if (line === 'остановить') {
                        return lines.length;
                    }

                    if (line.startsWith('подождать') || line.startsWith('задержка') || line.startsWith('пауза')) {
                        const match = line.match(/(подождать|задержка|пауза)\((\d+)\)/);
                        if (match) {
                            const ms = parseInt(match[2]);
                            const startTime = Date.now();
                            while (Date.now() - startTime < ms) {}
                        }
                        continue;
                    }

                    if (line === 'очистить') {
                        output.innerHTML = '';
                        continue;
                    }

                    if (line.includes('=') && !line.startsWith('если') && !line.startsWith('пока') &&
                        !line.startsWith('для') && !line.startsWith('функция') && !line.startsWith('константа')) {
                        const parts = line.split('=');
                        const name = parts[0].trim();
                        const value = parts.slice(1).join('=').trim();
                        variables[name] = getValue(value);
                        continue;
                    }

                    if (line.startsWith('константа')) {
                        const match = line.match(/константа\s+(\w+)\s*=\s*(.+)/);
                        if (match) {
                            const name = match[1];
                            const value = getValue(match[2].trim());
                            variables[name] = value;
                            Object.defineProperty(variables, name, { writable: false, configurable: false });
                        }
                        continue;
                    }

                    if (line.startsWith('если')) {
                        const match = line.match(/если\s+(.+?)\s+то/);
                        if (match) {
                            const condition = getValue(match[1].trim());
                            let level = 1;
                            let j = i;
                            let executed = false;

                            if (condition) {
                                executed = true;
                                let blockLines = [];
                                while (j < lines.length && level > 0) {
                                    const l = lines[j].trim();
                                    if (l.startsWith('если')) level++;
                                    else if (l === 'конец') {
                                        level--;
                                        if (level === 0) break;
                                    } else if (l === 'иначе' && level === 1) {
                                        break;
                                    } else if (level === 1) {
                                        blockLines.push(lines[j]);
                                    }
                                    j++;
                                }
                                let k = 0;
                                while (k < blockLines.length) {
                                    const bl = blockLines[k].trim();
                                    if (bl.includes('=') && !bl.startsWith('если') && !bl.startsWith('пока')) {
                                        const parts = bl.split('=');
                                        variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                    } else if (bl.startsWith('скажи')) {
                                        const m = bl.match(/скажи\((.*)\)/);
                                        if (m) log(String(getValue(m[1].trim())));
                                    } else if (bl.startsWith('спроси')) {
                                        const m = bl.match(/спроси\s+(\w+)/);
                                        if (m) {
                                            const val = prompt('Введите значение:');
                                            variables[m[1]] = val !== null ? val : '';
                                        }
                                    }
                                    k++;
                                }
                                i = j;
                            } else {
                                let level2 = 1;
                                while (j < lines.length) {
                                    const l = lines[j].trim();
                                    if (l.startsWith('если')) level2++;
                                    else if (l === 'конец') {
                                        level2--;
                                        if (level2 === 0) break;
                                    } else if (l === 'иначе' && level2 === 1) {
                                        j++;
                                        let blockLines2 = [];
                                        while (j < lines.length) {
                                            const l2 = lines[j].trim();
                                            if (l2 === 'конец') {
                                                i = j;
                                                break;
                                            }
                                            blockLines2.push(lines[j]);
                                            j++;
                                        }
                                        let k = 0;
                                        while (k < blockLines2.length) {
                                            const bl = blockLines2[k].trim();
                                            if (bl.includes('=') && !bl.startsWith('если')) {
                                                const parts = bl.split('=');
                                                variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                            } else if (bl.startsWith('скажи')) {
                                                const m = bl.match(/скажи\((.*)\)/);
                                                if (m) log(String(getValue(m[1].trim())));
                                            }
                                            k++;
                                        }
                                        break;
                                    }
                                    j++;
                                }
                            }
                            continue;
                        }
                    }

                    if (line.startsWith('иначе_если')) {
                        continue;
                    }

                    if (line.startsWith('выбор')) {
                        const match = line.match(/выбор\s+(\w+)/);
                        if (match) {
                            const varName = match[1];
                            const value = variables[varName];
                            let j = i;
                            let found = false;
                            while (j < lines.length) {
                                const l = lines[j].trim();
                                if (l === 'конец') {
                                    i = j;
                                    break;
                                }
                                if (l.startsWith('вариант')) {
                                    const m = l.match(/вариант\s+(.+?)\s*:/);
                                    if (m) {
                                        const caseVal = getValue(m[1].trim());
                                        if (value == caseVal && !found) {
                                            found = true;
                                            j++;
                                            while (j < lines.length) {
                                                const l2 = lines[j].trim();
                                                if (l2.startsWith('вариант') || l2 === 'иначе' || l2 === 'конец') {
                                                    break;
                                                }
                                                const bl = l2.trim();
                                                if (bl.includes('=') && !bl.startsWith('если')) {
                                                    const parts = bl.split('=');
                                                    variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                                } else if (bl.startsWith('скажи')) {
                                                    const m2 = bl.match(/скажи\((.*)\)/);
                                                    if (m2) log(String(getValue(m2[1].trim())));
                                                }
                                                j++;
                                            }
                                            continue;
                                        }
                                    }
                                }
                                if (l === 'иначе' && !found) {
                                    j++;
                                    while (j < lines.length) {
                                        const l2 = lines[j].trim();
                                        if (l2 === 'конец') break;
                                        const bl = l2.trim();
                                        if (bl.includes('=') && !bl.startsWith('если')) {
                                            const parts = bl.split('=');
                                            variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                        } else if (bl.startsWith('скажи')) {
                                            const m2 = bl.match(/скажи\((.*)\)/);
                                            if (m2) log(String(getValue(m2[1].trim())));
                                        }
                                        j++;
                                    }
                                    break;
                                }
                                j++;
                            }
                            continue;
                        }
                    }

                    if (line.startsWith('пока')) {
                        const match = line.match(/пока\s+(.+?)\s+то/);
                        if (match) {
                            let maxIter = 10000;
                            let iterations = 0;
                            while (getValue(match[1].trim()) && maxIter > 0) {
                                iterations++;
                                let j = i;
                                let level = 1;
                                while (j < lines.length && level > 0) {
                                    const l = lines[j].trim();
                                    if (l.startsWith('пока')) level++;
                                    else if (l === 'конец') {
                                        level--;
                                        if (level === 0) break;
                                    } else if (level === 1) {
                                        const bl = lines[j].trim();
                                        if (bl === 'прервать') {
                                            level = 0;
                                            break;
                                        }
                                        if (bl === 'продолжить') {
                                            j++;
                                            continue;
                                        }
                                        if (bl.includes('=') && !bl.startsWith('если') && !bl.startsWith('пока')) {
                                            const parts = bl.split('=');
                                            variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                        } else if (bl.startsWith('скажи')) {
                                            const m = bl.match(/скажи\((.*)\)/);
                                            if (m) log(String(getValue(m[1].trim())));
                                        } else if (bl.startsWith('спроси')) {
                                            const m = bl.match(/спроси\s+(\w+)/);
                                            if (m) {
                                                const val = prompt('Введите значение:');
                                                variables[m[1]] = val !== null ? val : '';
                                            }
                                        } else if (bl.startsWith('если')) {
                                            const m2 = bl.match(/если\s+(.+?)\s+то/);
                                            if (m2) {
                                                const cond = getValue(m2[1].trim());
                                                let level2 = 1;
                                                let k = j + 1;
                                                if (cond) {
                                                    while (k < lines.length && level2 > 0) {
                                                        const l2 = lines[k].trim();
                                                        if (l2.startsWith('если')) level2++;
                                                        else if (l2 === 'конец') {
                                                            level2--;
                                                            if (level2 === 0) break;
                                                        } else if (level2 === 1 && !l2.startsWith('иначе')) {
                                                            const bl2 = lines[k].trim();
                                                            if (bl2.includes('=') && !bl2.startsWith('если')) {
                                                                const parts2 = bl2.split('=');
                                                                variables[parts2[0].trim()] = getValue(parts2
                                                                    .slice(1).join('=').trim());
                                                            } else if (bl2.startsWith('скажи')) {
                                                                const m3 = bl2.match(/скажи\((.*)\)/);
                                                                if (m3) log(String(getValue(m3[1].trim())));
                                                            }
                                                        }
                                                        k++;
                                                    }
                                                } else {
                                                    while (k < lines.length && level2 > 0) {
                                                        const l2 = lines[k].trim();
                                                        if (l2.startsWith('если')) level2++;
                                                        else if (l2 === 'конец') {
                                                            level2--;
                                                            if (level2 === 0) break;
                                                        } else if (l2 === 'иначе' && level2 === 1) {
                                                            k++;
                                                            while (k < lines.length) {
                                                                const l3 = lines[k].trim();
                                                                if (l3 === 'конец') break;
                                                                const bl2 = l3.trim();
                                                                if (bl2.includes('=') && !bl2.startsWith('если')) {
                                                                    const parts2 = bl2.split('=');
                                                                    variables[parts2[0].trim()] = getValue(parts2
                                                                        .slice(1).join('=').trim());
                                                                } else if (bl2.startsWith('скажи')) {
                                                                    const m3 = bl2.match(/скажи\((.*)\)/);
                                                                    if (m3) log(String(getValue(m3[1].trim())));
                                                                }
                                                                k++;
                                                            }
                                                            break;
                                                        }
                                                        k++;
                                                    }
                                                }
                                                j = k;
                                            }
                                        } else if (bl === 'остановить') {
                                            return lines.length;
                                        }
                                    }
                                    j++;
                                }
                                maxIter--;
                            }
                            if (maxIter === 0) {
                                log('⚠️ Бесконечный цикл прерван!', 'info');
                            }
                            continue;
                        }
                    }

                    if (line.startsWith('для')) {
                        const match = line.match(/для\s+(\w+)\s+из\s+(.+?)\s+то/);
                        if (match) {
                            const list = getValue(match[2].trim());
                            if (Array.isArray(list)) {
                                for (const item of list) {
                                    variables[match[1]] = item;
                                    let j = i;
                                    let level = 1;
                                    while (j < lines.length && level > 0) {
                                        const l = lines[j].trim();
                                        if (l.startsWith('для')) level++;
                                        else if (l === 'конец') {
                                            level--;
                                            if (level === 0) break;
                                        } else if (level === 1) {
                                            const bl = lines[j].trim();
                                            if (bl === 'прервать') {
                                                level = 0;
                                                break;
                                            }
                                            if (bl === 'продолжить') {
                                                j++;
                                                continue;
                                            }
                                            if (bl.includes('=') && !bl.startsWith('если') && !bl.startsWith('для')) {
                                                const parts = bl.split('=');
                                                variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                            } else if (bl.startsWith('скажи')) {
                                                const m = bl.match(/скажи\((.*)\)/);
                                                if (m) log(String(getValue(m[1].trim())));
                                            } else if (bl.startsWith('спроси')) {
                                                const m = bl.match(/спроси\s+(\w+)/);
                                                if (m) {
                                                    const val = prompt('Введите значение:');
                                                    variables[m[1]] = val !== null ? val : '';
                                                }
                                            } else if (bl.startsWith('если')) {
                                                const m2 = bl.match(/если\s+(.+?)\s+то/);
                                                if (m2) {
                                                    const cond = getValue(m2[1].trim());
                                                    let level2 = 1;
                                                    let k = j + 1;
                                                    if (cond) {
                                                        while (k < lines.length && level2 > 0) {
                                                            const l2 = lines[k].trim();
                                                            if (l2.startsWith('если')) level2++;
                                                            else if (l2 === 'конец') {
                                                                level2--;
                                                                if (level2 === 0) break;
                                                            } else if (level2 === 1 && !l2.startsWith('иначе')) {
                                                                const bl2 = lines[k].trim();
                                                                if (bl2.includes('=') && !bl2.startsWith('если')) {
                                                                    const parts2 = bl2.split('=');
                                                                    variables[parts2[0].trim()] = getValue(parts2
                                                                        .slice(1).join('=').trim());
                                                                } else if (bl2.startsWith('скажи')) {
                                                                    const m3 = bl2.match(/скажи\((.*)\)/);
                                                                    if (m3) log(String(getValue(m3[1].trim())));
                                                                }
                                                            }
                                                            k++;
                                                        }
                                                    } else {
                                                        while (k < lines.length && level2 > 0) {
                                                            const l2 = lines[k].trim();
                                                            if (l2.startsWith('если')) level2++;
                                                            else if (l2 === 'конец') {
                                                                level2--;
                                                                if (level2 === 0) break;
                                                            } else if (l2 === 'иначе' && level2 === 1) {
                                                                k++;
                                                                while (k < lines.length) {
                                                                    const l3 = lines[k].trim();
                                                                    if (l3 === 'конец') break;
                                                                    const bl2 = l3.trim();
                                                                    if (bl2.includes('=') && !bl2.startsWith('если')) {
                                                                        const parts2 = bl2.split('=');
                                                                        variables[parts2[0].trim()] = getValue(parts2
                                                                            .slice(1).join('=').trim());
                                                                    } else if (bl2.startsWith('скажи')) {
                                                                        const m3 = bl2.match(/скажи\((.*)\)/);
                                                                        if (m3) log(String(getValue(m3[1].trim())));
                                                                    }
                                                                    k++;
                                                                }
                                                                break;
                                                            }
                                                            k++;
                                                        }
                                                    }
                                                    j = k;
                                                }
                                            }
                                        }
                                        j++;
                                    }
                                }
                            }
                            continue;
                        }
                    }

                    if (line.startsWith('функция')) {
                        const match = line.match(/функция\s+(\w+)\s*\(([^)]*)\)/);
                        if (match) {
                            const name = match[1];
                            const args = match[2].split(',').map(s => s.trim()).filter(Boolean);
                            let body = [];
                            let j = i;
                            while (j < lines.length) {
                                const l = lines[j].trim();
                                if (l === 'конец') break;
                                body.push(lines[j]);
                                j++;
                            }
                            functions[name] = { args, body };
                            i = j;
                            continue;
                        }
                    }

                    if (line.startsWith('вернуть')) {
                        continue;
                    }

                    if (line.startsWith('повторить')) {
                        const match = line.match(/повторить\((\d+)\)/);
                        if (match) {
                            const count = parseInt(match[1]);
                            let j = i;
                            let level = 1;
                            let blockLines = [];
                            while (j < lines.length && level > 0) {
                                const l = lines[j].trim();
                                if (l.startsWith('повторить')) level++;
                                else if (l === 'конец') {
                                    level--;
                                    if (level === 0) break;
                                } else if (level === 1) {
                                    blockLines.push(lines[j]);
                                }
                                j++;
                            }
                            for (let iter = 0; iter < count; iter++) {
                                let k = 0;
                                while (k < blockLines.length) {
                                    const bl = blockLines[k].trim();
                                    if (bl.includes('=') && !bl.startsWith('если') && !bl.startsWith('повторить')) {
                                        const parts = bl.split('=');
                                        variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                    } else if (bl.startsWith('скажи')) {
                                        const m = bl.match(/скажи\((.*)\)/);
                                        if (m) log(String(getValue(m[1].trim())));
                                    }
                                    k++;
                                }
                            }
                            i = j;
                            continue;
                        }
                    }

                    if (line === 'прервать') {
                        continue;
                    }

                    if (line === 'продолжить') {
                        continue;
                    }

                    if (line.startsWith('цвет')) {
                        const match = line.match(/цвет\(["'](.+?)["']\)/);
                        if (match) {
                            const colors = {
                                'красный': '#ff6b6b',
                                'зелёный': '#7bed9f',
                                'синий': '#7b9fff',
                                'жёлтый': '#ffd93d',
                                'оранжевый': '#ff9f43',
                                'фиолетовый': '#7b2ffc',
                                'розовый': '#ff6b9d',
                                'белый': '#ffffff',
                                'чёрный': '#000000'
                            };
                            const color = colors[match[1]] || '#ffffff';
                            output.style.color = color;
                        }
                        continue;
                    }

                    if (line.startsWith('цвет_фона')) {
                        const match = line.match(/цвет_фона\(["'](.+?)["']\)/);
                        if (match) {
                            const colors = {
                                'красный': '#ff6b6b',
                                'зелёный': '#7bed9f',
                                'синий': '#7b9fff',
                                'жёлтый': '#ffd93d',
                                'оранжевый': '#ff9f43',
                                'фиолетовый': '#7b2ffc',
                                'розовый': '#ff6b9d',
                                'белый': '#ffffff',
                                'чёрный': '#000000'
                            };
                            const color = colors[match[1]] || '#000000';
                            output.style.background = color;
                        }
                        continue;
                    }

                    if (line === 'скинуть_цвет()' || line === 'скинуть_цвет') {
                        output.style.color = '#7bed9f';
                        output.style.background = '#0a0e17';
                        continue;
                    }

                    if (line.startsWith('прогресс')) {
                        const match = line.match(/прогресс\((\d+)\s*,\s*(\d+)\)/);
                        if (match) {
                            const current = parseInt(match[1]);
                            const max = parseInt(match[2]);
                            const percent = Math.round((current / max) * 100);
                            const bar = '█'.repeat(Math.floor(percent / 2)) + '░'.repeat(50 - Math.floor(percent / 2));
                            log(`[${bar}] ${percent}%`, 'info');
                        }
                        continue;
                    }

                    if (line === 'попробовать') {
                        let j = i;
                        let level = 1;
                        while (j < lines.length && level > 0) {
                            const l = lines[j].trim();
                            if (l === 'попробовать') level++;
                            else if (l === 'поймать') {
                                level--;
                                if (level === 0) break;
                            }
                            j++;
                        }
                        let catchLevel = 1;
                        while (j < lines.length && catchLevel > 0) {
                            const l = lines[j].trim();
                            if (l === 'поймать') catchLevel++;
                            else if (l === 'конец') {
                                catchLevel--;
                                if (catchLevel === 0) break;
                            }
                            j++;
                        }
                        i = j;
                        continue;
                    }

                    if (line.startsWith('вызвать_ошибку')) {
                        const match = line.match(/вызвать_ошибку\(["'](.+?)["']\)/);
                        if (match) {
                            throw new Error(match[1]);
                        }
                        continue;
                    }

                    if (line.startsWith('отладка')) {
                        const match = line.match(/отладка\((\w+)\)/);
                        if (match) {
                            const name = match[1];
                            const val = variables[name];
                            log(`🔍 ${name} = ${val !== undefined ? JSON.stringify(val) : 'не определена'}`, 'info');
                        }
                        continue;
                    }

                    if (line === 'ждать_нажатие()') {
                        alert('Нажмите OK чтобы продолжить...');
                        continue;
                    }

                    if (line.startsWith('время_выполнения')) {
                        const match = line.match(/время_выполнения\((\w+)\)/);
                        if (match) {
                            const funcName = match[1];
                            if (functions[funcName]) {
                                const startTime = performance.now();
                                const func = functions[funcName];
                                const oldVars = { ...variables };
                                let result = null;
                                let returned = false;
                                let k = 0;
                                while (k < func.body.length && !returned) {
                                    const l = func.body[k].trim();
                                    if (l.startsWith('вернуть')) {
                                        const m = l.match(/вернуть\s+(.+)/);
                                        if (m) {
                                            result = getValue(m[1].trim());
                                            returned = true;
                                        }
                                    } else {
                                        if (l.includes('=') && !l.startsWith('если')) {
                                            const parts = l.split('=');
                                            variables[parts[0].trim()] = getValue(parts.slice(1).join('=').trim());
                                        } else if (l.startsWith('скажи')) {
                                            const m = l.match(/скажи\((.*)\)/);
                                            if (m) log(String(getValue(m[1].trim())));
                                        }
                                    }
                                    k++;
                                }
                                Object.assign(variables, oldVars);
                                const elapsed = Math.round(performance.now() - startTime);
                                log(`⏱ Время выполнения: ${elapsed}ms`, 'info');
                                return result !== null ? result : '';
                            }
                        }
                        continue;
                    }

                    if (line.startsWith('проверить_тип')) {
                        const match = line.match(/проверить_тип\((\w+)\s*,\s*["'](.+?)["']\)/);
                        if (match) {
                            const val = variables[match[1]];
                            const type = match[2];
                            const actualType = Array.isArray(val) ? 'список' : typeof val;
                            return actualType === type;
                        }
                        continue;
                    }

                    if (line.startsWith('преобразовать_в_число')) {
                        const match = line.match(/преобразовать_в_число\(["'](.+?)["']\)/);
                        if (match) {
                            return parseFloat(match[1]) || 0;
                        }
                        continue;
                    }

                    if (line.startsWith('преобразовать_в_строку')) {
                        const match = line.match(/преобразовать_в_строку\((.+)\)/);
                        if (match) {
                            return String(getValue(match[1].trim()));
                        }
                        continue;
                    }

                    if (line.startsWith('рандомное_имя')) {
                        const chars = 'abcdefghijklmnopqrstuvwxyz';
                        let name = '';
                        for (let i = 0; i < 8; i++) {
                            name += chars[Math.floor(Math.random() * chars.length)];
                        }
                        return name;
                    }
                }
                return i;
            }

            try {
                const lines = code.split('\n');
                execute(lines, 0);
                if (outputText.length === 0) {
                    const div = document.createElement('div');
                    div.className = 'info';
                    div.textContent = '✅ Программа выполнена (нет вывода)';
                    output.appendChild(div);
                }
                const end = performance.now();
                timeInfo.textContent = `⏱ ${Math.round(end - start)}ms`;
                status.textContent = '✅ готово';
                status.style.color = '#7bed9f';
            } catch (e) {
                const end = performance.now();
                timeInfo.textContent = `⏱ ${Math.round(end - start)}ms`;
                const div = document.createElement('div');
                div.className = 'error';
                div.textContent = '❌ Ошибка: ' + e.message;
                output.appendChild(div);
                status.textContent = '❌ ошибка';
                status.style.color = '#ff6b6b';
                console.error(e);
            }
        }

        function clearOutput() {
            const output = document.getElementById('output');
            output.innerHTML = '';
            const status = document.getElementById('statusBadge');
            status.textContent = 'готов';
            status.style.color = '#7b8baa';
        }

        function saveCode() {
            const code = document.getElementById('code').value;
            const blob = new Blob([code], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'программа.тритон';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            setTimeout(() => URL.revokeObjectURL(url), 1000);
        }

        function loadCode() {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = '.тритон,.txt';
            input.onchange = function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        document.getElementById('code').value = event.target.result;
                        runCode();
                    };
                    reader.readAsText(file);
                }
            };
            input.click();
        }

        // ================================================================
        // ДОКУМЕНТАЦИЯ
        // ================================================================

        function renderDocs(filter = '') {
            const grid = document.getElementById('docGrid');
            const count = document.getElementById('docCount');
            grid.innerHTML = '';

            const filtered = filter ?
                commands.filter(c =>
                    c.cmd.toLowerCase().includes(filter.toLowerCase()) ||
                    c.desc.toLowerCase().includes(filter.toLowerCase()) ||
                    c.tags.some(t => t.toLowerCase().includes(filter.toLowerCase()))
                ) :
                commands;

            count.textContent = `Всего команд: ${filtered.length} из ${commands.length}`;

            if (filtered.length === 0) {
                grid.innerHTML =
                    `<div style="grid-column:1/-1; text-align:center; padding:40px; color:#5a6a8a;">
                        🔍 Ничего не найдено по запросу "${filter}"
                    </div>`;
                return;
            }

            for (const cmd of filtered) {
                const card = document.createElement('div');
                card.className = 'doc-card';

                const cmdHtml = cmd.cmd
                    .replace(/(скажи|спроси|если|то|иначе|конец|пока|для|из|функция|вернуть|остановить|подождать|очистить|прервать|продолжить|повторить|открыть|закрыть|прочитать|записать|дописать|существует|удалить|добавить|вставить|длина|содержит|срез|верх|низ|заменить|разделить|объединить|подстрока|абс|округлить|случайное|случайный_выбор|сейчас|год|месяц|день|часы|минуты|секунды|день_недели|формат_даты|запросить|отправить_данные|команда|переменная_окружения|текущая_папка|сменить_папку|список_файлов|цвет|цвет_фона|скинуть_цвет|прогресс|попробовать|поймать|вызвать_ошибку|тип_ошибки|отладка|ждать_нажатие|время_выполнения|проверить_тип|преобразовать_в_число|преобразовать_в_строку|рандомное_имя|сортировать|сортировать_по|перевернуть|константа|скопировать|иначе_если|выбор|вариант|сумма|среднее|максимум|минимум|степень|корень|логарифм|синус|косинус|тангенс|экспонента|факториал|дробная_часть|целая_часть|json_парсить|json_строка|цвет_текста|сбросить_цвета|задержка|пауза|вывод|печать|показать)/g,
                        '<span class="kw">$1</span>');

                card.innerHTML = `
                    <div class="cmd">${cmdHtml}</div>
                    <div class="desc">${cmd.desc}</div>
                    <div class="example">${cmd.example}</div>
                    <div class="tags">
                        ${cmd.tags.map(t => `<span class="tag">${t}</span>`).join('')}
                        <span class="tag primary">${cmd.tags.length} тега</span>
                    </div>
                `;
                grid.appendChild(card);
            }
        }

        function searchDocs() {
            const input = document.getElementById('docSearch');
            renderDocs(input.value);
        }

        // ================================================================
        // ВКЛАДКИ
        // ================================================================

        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
                document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                this.classList.add('active');
                document.getElementById('tab-' + this.dataset.tab).classList.add('active');
            });
        });

        // ================================================================
        // ГОРЯЧИЕ КЛАВИШИ
        // ================================================================

        document.addEventListener('keydown', function(e) {
            if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) {
                e.preventDefault();
                runCode();
            }
        });

        // ================================================================
        // ИНИЦИАЛИЗАЦИЯ
        // ================================================================

        window.onload = function() {
            renderDocs();
            setTimeout(runCode, 500);
            console.log('🐚 Тритон загружен!');
            console.log(`📚 Всего команд: ${commands.length}`);
            console.log('▶️ Нажми Ctrl+Enter для запуска');
            console.log('🖼️ Логотип Тритона ВСТРОЕН НАВСЕГДА!');
        };
    </script>

</body>
</html>

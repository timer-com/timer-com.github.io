<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SiteCraft — Конструктор сайтов</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #0a0e17;
            color: #e6edf3;
            height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .topbar {
            background: #161b22;
            border-bottom: 1px solid #30363d;
            padding: 12px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            z-index: 10;
            flex-shrink: 0;
        }

        .topbar .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 22px;
            font-weight: 700;
            background: linear-gradient(135deg, #58a6ff, #3fb950);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .topbar .actions {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 8px 20px;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary {
            background: #238636;
            color: white;
        }
        .btn-primary:hover {
            background: #2ea043;
            transform: scale(1.02);
        }

        .btn-success {
            background: #1f6feb;
            color: white;
        }
        .btn-success:hover {
            background: #388bfd;
            transform: scale(1.02);
        }

        .btn-danger {
            background: #da3633;
            color: white;
        }
        .btn-danger:hover {
            background: #f85149;
        }

        .btn-outline {
            background: transparent;
            border: 1px solid #30363d;
            color: #e6edf3;
        }
        .btn-outline:hover {
            border-color: #58a6ff;
        }

        .btn-publish {
            background: #d29922;
            color: #0a0e17;
        }
        .btn-publish:hover {
            background: #e3b341;
            transform: scale(1.02);
        }

        .main {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        .sidebar {
            width: 260px;
            background: #161b22;
            border-right: 1px solid #30363d;
            padding: 15px;
            overflow-y: auto;
            flex-shrink: 0;
        }

        .sidebar h3 {
            font-size: 14px;
            color: #8b949e;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 12px;
        }

        .element-list {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }

        .element-item {
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 8px;
            padding: 12px 8px;
            text-align: center;
            cursor: grab;
            transition: all 0.2s;
            font-size: 13px;
            user-select: none;
        }

        .element-item:hover {
            border-color: #58a6ff;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(88, 166, 255, 0.15);
        }

        .element-item .icon {
            font-size: 28px;
            display: block;
            margin-bottom: 4px;
        }

        .canvas-wrapper {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            background: #0d1117;
            height: 100%;
        }

        /* Стили для скролла канваса */
        .canvas-wrapper::-webkit-scrollbar {
            width: 10px;
        }
        .canvas-wrapper::-webkit-scrollbar-track {
            background: #0d1117;
        }
        .canvas-wrapper::-webkit-scrollbar-thumb {
            background: #30363d;
            border-radius: 5px;
        }
        .canvas-wrapper::-webkit-scrollbar-thumb:hover {
            background: #484f58;
        }

        .canvas {
            max-width: 1000px;
            margin: 0 auto;
            background: #ffffff;
            color: #1f2937;
            border-radius: 12px;
            box-shadow: 0 8px 40px rgba(0, 0, 0, 0.5);
            min-height: 600px;
            padding: 40px 50px;
            position: relative;
            transition: all 0.2s;
        }

        .canvas .empty-state {
            text-align: center;
            color: #9ca3af;
            padding: 80px 20px;
            font-size: 18px;
        }

        .canvas .empty-state .big {
            font-size: 64px;
            display: block;
            margin-bottom: 20px;
        }

        .canvas-element {
            position: relative;
            margin: 8px 0;
            padding: 8px 12px;
            border-radius: 6px;
            border: 2px solid transparent;
            transition: all 0.15s;
            cursor: pointer;
        }

        .canvas-element:hover {
            border-color: #58a6ff;
            background: rgba(88, 166, 255, 0.05);
        }

        .canvas-element.selected {
            border-color: #1f6feb;
            background: rgba(88, 166, 255, 0.1);
            box-shadow: 0 0 0 3px rgba(88, 166, 255, 0.2);
        }

        .canvas-element .delete-btn {
            position: absolute;
            top: -10px;
            right: -10px;
            background: #da3633;
            color: white;
            border: none;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            font-size: 14px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
        }

        .canvas-element:hover .delete-btn {
            display: flex;
        }

        .canvas-element[data-type="heading"] {
            font-size: 32px;
            font-weight: 700;
        }
        .canvas-element[data-type="subheading"] {
            font-size: 24px;
            font-weight: 600;
        }
        .canvas-element[data-type="text"] {
            font-size: 16px;
            line-height: 1.6;
        }
        .canvas-element[data-type="button"] {
            display: inline-block;
            background: #1f6feb;
            color: white !important;
            padding: 12px 30px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            border: none;
        }
        .canvas-element[data-type="image-placeholder"] {
            background: #f3f4f6;
            padding: 40px;
            text-align: center;
            border: 2px dashed #d1d5db;
            border-radius: 8px;
            color: #6b7280;
        }
        .canvas-element[data-type="image-placeholder"] img {
            max-width: 100%;
            border-radius: 8px;
        }
        .canvas-element[data-type="divider"] {
            border: none;
            border-top: 2px solid #e5e7eb;
            padding: 0;
            height: 2px;
            margin: 20px 0;
        }
        .canvas-element[data-type="input"] input {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
        }
        .canvas-element[data-type="input"] input:focus {
            outline: none;
            border-color: #1f6feb;
        }
        .canvas-element[data-type="textarea"] textarea {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
            min-height: 100px;
            resize: vertical;
            font-family: inherit;
        }
        .canvas-element[data-type="textarea"] textarea:focus {
            outline: none;
            border-color: #1f6feb;
        }
        .canvas-element[data-type="card"] {
            background: #f9fafb;
            border: 1px solid #e5e7eb;
            padding: 20px;
            border-radius: 12px;
        }

        .properties-panel {
            width: 280px;
            background: #161b22;
            border-left: 1px solid #30363d;
            padding: 15px;
            overflow-y: auto;
            flex-shrink: 0;
            display: none;
        }

        .properties-panel.active {
            display: block;
        }

        .properties-panel h3 {
            font-size: 14px;
            color: #8b949e;
            text-transform: uppercase;
            margin-bottom: 12px;
        }

        .prop-group {
            margin-bottom: 15px;
        }

        .prop-group label {
            display: block;
            font-size: 13px;
            color: #8b949e;
            margin-bottom: 4px;
        }

        .prop-group input,
        .prop-group select,
        .prop-group textarea {
            width: 100%;
            padding: 8px 12px;
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 6px;
            color: #e6edf3;
            font-size: 14px;
            font-family: inherit;
        }

        .prop-group input:focus,
        .prop-group select:focus,
        .prop-group textarea:focus {
            outline: none;
            border-color: #58a6ff;
        }

        .prop-group .color-picker {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .prop-group .color-picker input[type="color"] {
            width: 40px;
            height: 40px;
            padding: 2px;
            border-radius: 6px;
            cursor: pointer;
        }

        .publish-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .publish-modal.active {
            display: flex;
        }

        .publish-modal .content {
            background: #161b22;
            border: 1px solid #30363d;
            border-radius: 16px;
            max-width: 550px;
            width: 100%;
            padding: 35px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .publish-modal .content h2 {
            margin-bottom: 10px;
            font-size: 28px;
        }
        .publish-modal .content .sub {
            color: #8b949e;
            margin-bottom: 20px;
        }

        .publish-modal .content .link-box {
            background: #0d1117;
            padding: 15px 20px;
            border-radius: 8px;
            margin: 15px 0;
            word-break: break-all;
            font-family: 'Courier New', monospace;
            font-size: 18px;
            color: #58a6ff;
            border: 1px solid #30363d;
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 10px;
        }

        .publish-modal .content .link-box .copy-btn {
            background: #21262d;
            border: none;
            color: #e6edf3;
            padding: 6px 12px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 13px;
            white-space: nowrap;
        }

        .publish-modal .content .link-box .copy-btn:hover {
            background: #30363d;
        }

        .publish-modal .content .status {
            padding: 12px;
            border-radius: 8px;
            margin: 15px 0;
            display: none;
        }

        .publish-modal .content .status.success {
            display: block;
            background: rgba(35, 134, 54, 0.2);
            border: 1px solid #238636;
            color: #3fb950;
        }

        .publish-modal .content .status.error {
            display: block;
            background: rgba(218, 54, 51, 0.2);
            border: 1px solid #da3633;
            color: #f85149;
        }

        .publish-modal .content .status.loading {
            display: block;
            background: rgba(88, 166, 255, 0.1);
            border: 1px solid #58a6ff;
            color: #58a6ff;
        }

        .publish-modal .content .btn {
            width: 100%;
            margin-top: 10px;
        }
        .publish-modal .content .view-btn {
            background: #1f6feb;
            color: white;
        }
        .publish-modal .content .view-btn:hover {
            background: #388bfd;
        }

        .github-token-input {
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 8px;
            padding: 12px 16px;
            color: #e6edf3;
            width: 100%;
            font-size: 14px;
            margin: 10px 0;
        }

        .github-token-input:focus {
            outline: none;
            border-color: #58a6ff;
        }

        /* Счётчик элементов */
        .element-counter {
            background: #21262d;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 13px;
            color: #8b949e;
            margin-left: 10px;
        }

        @media (max-width: 768px) {
            .sidebar {
                width: 200px;
            }
            .properties-panel {
                width: 220px;
            }
            .canvas {
                padding: 20px;
            }
            .element-list {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 600px) {
            .main {
                flex-direction: column;
            }
            .sidebar {
                width: 100%;
                border-right: none;
                border-bottom: 1px solid #30363d;
                max-height: 180px;
            }
            .properties-panel {
                width: 100%;
                border-left: none;
                border-top: 1px solid #30363d;
            }
            .topbar .actions .btn {
                font-size: 12px;
                padding: 6px 12px;
            }
            .publish-modal .content {
                padding: 20px;
            }
            .publish-modal .content .link-box {
                font-size: 14px;
                flex-wrap: wrap;
            }
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
        .canvas-element {
            animation: fadeIn 0.3s ease;
        }

        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0d1117;
        }
        ::-webkit-scrollbar-thumb {
            background: #30363d;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #484f58;
        }
    </style>
</head>
<body>
    <div class="topbar">
        <div class="logo">🚀 SiteCraft</div>
        <div class="actions">
            <span class="element-counter" id="elementCounter">0 элементов</span>
            <button class="btn btn-outline" onclick="clearCanvas()">🗑 Очистить</button>
            <button class="btn btn-publish" onclick="showPublishModal()">🌐 Опубликовать</button>
            <button class="btn btn-success" onclick="exportHTML()">💾 Скачать HTML</button>
        </div>
    </div>

    <div class="main">
        <div class="sidebar">
            <h3>📦 Элементы</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="heading" data-content="Заголовок H1">
                    <span class="icon">📰</span> Заголовок
                </div>
                <div class="element-item" draggable="true" data-type="subheading" data-content="Подзаголовок H2">
                    <span class="icon">📝</span> Подзаголовок
                </div>
                <div class="element-item" draggable="true" data-type="text" data-content="Текст абзаца...">
                    <span class="icon">📄</span> Текст
                </div>
                <div class="element-item" draggable="true" data-type="button" data-content="Кнопка">
                    <span class="icon">🔘</span> Кнопка
                </div>
                <div class="element-item" draggable="true" data-type="image-placeholder" data-content="https://via.placeholder.com/600x300">
                    <span class="icon">🖼️</span> Картинка
                </div>
                <div class="element-item" draggable="true" data-type="divider" data-content="">
                    <span class="icon">➖</span> Разделитель
                </div>
                <div class="element-item" draggable="true" data-type="input" data-content="Введите текст...">
                    <span class="icon">✏️</span> Поле ввода
                </div>
                <div class="element-item" draggable="true" data-type="textarea" data-content="Введите текст...">
                    <span class="icon">📋</span> Текстовая область
                </div>
                <div class="element-item" draggable="true" data-type="card" data-content="Карточка">
                    <span class="icon">📇</span> Карточка
                </div>
            </div>
        </div>

        <div class="canvas-wrapper" id="canvasWrapper">
            <div class="canvas" id="canvas">
                <div class="empty-state" id="emptyState">
                    <span class="big">🎨</span>
                    Перетащи элемент с панели слева<br>
                    или кликни на элемент для редактирования
                </div>
            </div>
        </div>

        <div class="properties-panel" id="propertiesPanel">
            <h3>⚙️ Свойства</h3>
            <div class="prop-group">
                <label>Текст</label>
                <input type="text" id="propText" onchange="updateSelectedElement('text', this.value)">
            </div>
            <div class="prop-group">
                <label>Цвет текста</label>
                <div class="color-picker">
                    <input type="color" id="propColor" onchange="updateSelectedElement('color', this.value)">
                    <span style="font-size:13px; color:#8b949e;" id="colorValue">#ffffff</span>
                </div>
            </div>
            <div class="prop-group">
                <label>Размер (px)</label>
                <input type="number" id="propSize" onchange="updateSelectedElement('size', this.value + 'px')">
            </div>
            <div class="prop-group">
                <label>Выравнивание</label>
                <select id="propAlign" onchange="updateSelectedElement('align', this.value)">
                    <option value="left">По левому краю</option>
                    <option value="center">По центру</option>
                    <option value="right">По правому краю</option>
                </select>
            </div>
            <div class="prop-group">
                <label>Фон</label>
                <div class="color-picker">
                    <input type="color" id="propBg" onchange="updateSelectedElement('bg', this.value)">
                </div>
            </div>
            <button class="btn btn-danger" style="width:100%; margin-top:10px;" onclick="deleteSelected()">
                🗑 Удалить элемент
            </button>
        </div>
    </div>

    <!-- Модалка публикации -->
    <div class="publish-modal" id="publishModal">
        <div class="content">
            <h2>🌐 Публикация сайта</h2>
            <p class="sub">Для публикации используем GitHub Gist (бесплатно). Введите токен GitHub.</p>

            <div style="background:#1c2333; padding:15px; border-radius:8px; margin-bottom:15px; border-left:3px solid #d29922;">
                <p style="color:#8b949e; font-size:13px; margin-bottom:8px;">
                    🔑 <strong>Как получить токен:</strong>
                </p>
                <ol style="color:#8b949e; font-size:13px; padding-left:20px; line-height:1.8;">
                    <li>Зайдите на <a href="https://github.com/settings/tokens" target="_blank" style="color:#58a6ff;">github.com/settings/tokens</a></li>
                    <li>Нажмите "Generate new token (classic)"</li>
                    <li>Отметьте "gist" в списке разрешений</li>
                    <li>Скопируйте токен и вставьте ниже</li>
                </ol>
            </div>

            <input type="password" class="github-token-input" id="githubToken"
            placeholder="Введите GitHub токен..." value="">

            <div style="display:flex; gap:10px; margin:10px 0;">
                <button class="btn btn-primary" onclick="publishToGist()" style="flex:1;">
                    🚀 Опубликовать
                </button>
                <button class="btn btn-outline" onclick="loadFromGist()" style="flex:1;">
                    📥 Загрузить
                </button>
            </div>

            <div class="status" id="publishStatus"></div>

            <div id="publishedLinkContainer" style="display:none;">
                <div class="link-box">
                    <span id="publishedLink">https://gist.github.com/...</span>
                    <button class="copy-btn" onclick="copyLink()">📋 Копировать</button>
                </div>
                <button class="btn view-btn" onclick="openPublishedSite()">🔗 Открыть сайт</button>
            </div>

            <button class="btn btn-outline" onclick="closePublish()" style="margin-top:10px;">✕ Закрыть</button>
        </div>
    </div>

    <script>
        // ============================================
        //  СОСТОЯНИЕ
        // ============================================
        let elements = [];
        let selectedId = null;
        let elementIdCounter = 0;
        let gistId = null;

        // ============================================
        //  ГЕНЕРАЦИЯ HTML
        // ============================================
        function generateHTML() {
            const sorted = [...elements].sort((a, b) => a.order - b.order);
            let bodyContent = sorted.map(el => {
                let style = '';
                if (el.style) {
                    if (el.style.color) style += `color:${el.style.color};`;
                    if (el.style.fontSize) style += `font-size:${el.style.fontSize};`;
                    if (el.style.textAlign) style += `text-align:${el.style.textAlign};`;
                    if (el.style.background && el.style.background !== 'transparent' && el.style.background !==
                        '#ffffff') {
                        style += `background:${el.style.background};padding:15px;border-radius:8px;`;
                    }
                }
                const styleAttr = style ? ` style="${style}"` : '';

                switch (el.type) {
                    case 'heading':
                        return `<h1${styleAttr}>${el.content}</h1>`;
                    case 'subheading':
                        return `<h2${styleAttr}>${el.content}</h2>`;
                    case 'text':
                        return `<p${styleAttr}>${el.content}</p>`;
                    case 'button':
                        return `<button style="background:#1f6feb;color:white;padding:12px 30px;border:none;border-radius:8px;font-weight:600;cursor:pointer;">${el.content}</button>`;
                    case 'image-placeholder':
                        return `<img src="${el.content}" alt="Image" style="max-width:100%;border-radius:8px;">`;
                    case 'divider':
                        return `<hr style="border:none;border-top:2px solid #e5e7eb;margin:20px 0;">`;
                    case 'input':
                        return `<input type="text" placeholder="${el.content}" style="width:100%;padding:12px 16px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                    case 'textarea':
                        return `<textarea placeholder="${el.content}" style="width:100%;padding:12px 16px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;min-height:100px;resize:vertical;font-family:inherit;"></textarea>`;
                    case 'card':
                        return `<div style="background:#f9fafb;border:1px solid #e5e7eb;padding:20px;border-radius:12px;">${el.content}</div>`;
                    default:
                        return `<div${styleAttr}>${el.content}</div>`;
                }
            }).join('\n');

            return `<!DOCTYPE html>
        <html lang="ru">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Мой сайт на SiteCraft</title>
            <style>
                body {
                    max-width: 1000px;
                    margin: 40px auto;
                    padding: 0 20px;
                    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
                    line-height: 1.6;
                }
                * { box-sizing: border-box; }
                img { max-width: 100%; }
                button { cursor: pointer; }
                input, textarea { font-family: inherit; }
            </style>
        </head>
        <body>
            ${bodyContent}
        </body>
        </html>`;
        }

        // ============================================
        //  ПУБЛИКАЦИЯ В GITHUB GIST
        // ============================================
        async function publishToGist() {
            const token = document.getElementById('githubToken').value.trim();
            if (!token) {
                alert('⚠️ Введите GitHub токен!');
                return;
            }

            const status = document.getElementById('publishStatus');
            const linkContainer = document.getElementById('publishedLinkContainer');
            linkContainer.style.display = 'none';

            status.className = 'status loading';
            status.textContent = '⏳ Публикация на GitHub Gist...';

            try {
                const html = generateHTML();
                const filename = `site-${Date.now()}.html`;

                const url = gistId ?
                    `https://api.github.com/gists/${gistId}` :
                    'https://api.github.com/gists';

                const method = gistId ? 'PATCH' : 'POST';

                const body = {
                    description: 'Сайт создан в SiteCraft',
                    public: true,
                    files: {
                        [filename]: {
                            content: html
                        }
                    }
                };

                if (gistId) {
                    const oldGist = await fetch(`https://api.github.com/gists/${gistId}`, {
                        headers: { 'Authorization': `token ${token}` }
                    });
                    const oldData = await oldGist.json();
                    if (oldData.files) {
                        for (const [name, file] of Object.entries(oldData.files)) {
                            if (name !== filename) {
                                body.files[name] = { content: file.content };
                            }
                        }
                    }
                }

                const response = await fetch(url, {
                    method: method,
                    headers: {
                        'Authorization': `token ${token}`,
                        'Content-Type': 'application/json',
                        'Accept': 'application/vnd.github.v3+json'
                    },
                    body: JSON.stringify(body)
                });

                if (!response.ok) {
                    const error = await response.json();
                    throw new Error(error.message || 'Ошибка публикации');
                }

                const data = await response.json();
                gistId = data.id;

                try {
                    localStorage.setItem('sitecraft_gist_id', gistId);
                    localStorage.setItem('sitecraft_token', token);
                } catch (e) {}

                const rawUrl = `https://gist.githubusercontent.com/raw/${gistId}/${filename}`;
                const gistUrl = data.html_url;

                document.getElementById('publishedLink').textContent = rawUrl;
                linkContainer.style.display = 'block';

                status.className = 'status success';
                status.textContent = `✅ Сайт опубликован! Откройте по ссылке ниже.`;

                setTimeout(() => {
                    window.open(rawUrl, '_blank');
                }, 1000);

            } catch (error) {
                status.className = 'status error';
                status.textContent = `❌ Ошибка: ${error.message}`;
                console.error('Ошибка публикации:', error);
            }
        }

        // ============================================
        //  ЗАГРУЗКА ИЗ GIST
        // ============================================
        async function loadFromGist() {
            const token = document.getElementById('githubToken').value.trim();
            if (!token) {
                alert('⚠️ Введите GitHub токен!');
                return;
            }

            const status = document.getElementById('publishStatus');
            status.className = 'status loading';
            status.textContent = '⏳ Загрузка с GitHub Gist...';

            try {
                const response = await fetch('https://api.github.com/gists', {
                    headers: {
                        'Authorization': `token ${token}`,
                        'Accept': 'application/vnd.github.v3+json'
                    }
                });

                if (!response.ok) throw new Error('Ошибка загрузки списка');

                const gists = await response.json();
                const siteGist = gists.find(g => g.description === 'Сайт создан в SiteCraft');

                if (!siteGist) {
                    status.className = 'status error';
                    status.textContent = '❌ Не найден опубликованный сайт. Сначала опубликуйте.';
                    return;
                }

                gistId = siteGist.id;

                let htmlFile = null;
                for (const [name, file] of Object.entries(siteGist.files)) {
                    if (name.endsWith('.html')) {
                        htmlFile = file;
                        break;
                    }
                }

                if (!htmlFile) {
                    status.className = 'status error';
                    status.textContent = '❌ HTML файл не найден в Gist';
                    return;
                }

                const contentResponse = await fetch(htmlFile.raw_url);
                const htmlContent = await contentResponse.text();

                const bodyMatch = htmlContent.match(/<body>([\s\S]*?)<\/body>/i);
                if (bodyMatch) {
                    const body = bodyMatch[1];
                    const parser = new DOMParser();
                    const doc = parser.parseFromString(body, 'text/html');
                    const children = doc.body.children;

                    elements = [];
                    let order = 0;

                    for (const child of children) {
                        let type = 'text';
                        let content = child.textContent.trim();

                        if (child.tagName === 'H1') type = 'heading';
                        else if (child.tagName === 'H2') type = 'subheading';
                        else if (child.tagName === 'P') type = 'text';
                        else if (child.tagName === 'BUTTON') type = 'button';
                        else if (child.tagName === 'IMG') {
                            type = 'image-placeholder';
                            content = child.src;
                        } else if (child.tagName === 'HR') type = 'divider';
                        else if (child.tagName === 'INPUT') type = 'input';
                        else if (child.tagName === 'TEXTAREA') type = 'textarea';
                        else if (child.className && child.className.includes('card')) type = 'card';

                        const style = {
                            color: '#1f2937',
                            fontSize: '16px',
                            textAlign: 'left',
                            background: 'transparent'
                        };

                        if (child.style) {
                            if (child.style.color) style.color = child.style.color;
                            if (child.style.fontSize) style.fontSize = child.style.fontSize;
                            if (child.style.textAlign) style.textAlign = child.style.textAlign;
                            if (child.style.background) style.background = child.style.background;
                        }

                        elements.push({
                            id: ++elementIdCounter,
                            type: type,
                            content: content || ' ',
                            order: order++,
                            style: style
                        });
                    }

                    renderCanvas();
                    status.className = 'status success';
                    status.textContent = `✅ Загружено ${elements.length} элементов!`;

                    try {
                        localStorage.setItem('sitecraft_gist_id', gistId);
                        localStorage.setItem('sitecraft_token', token);
                    } catch (e) {}
                }

            } catch (error) {
                status.className = 'status error';
                status.textContent = `❌ Ошибка: ${error.message}`;
                console.error('Ошибка загрузки:', error);
            }
        }

        // ============================================
        //  УПРАВЛЕНИЕ МОДАЛКОЙ
        // ============================================
        function showPublishModal() {
            const modal = document.getElementById('publishModal');
            modal.classList.add('active');

            try {
                const savedToken = localStorage.getItem('sitecraft_token');
                if (savedToken) {
                    document.getElementById('githubToken').value = savedToken;
                }
            } catch (e) {}
        }

        function closePublish() {
            document.getElementById('publishModal').classList.remove('active');
        }

        function copyLink() {
            const link = document.getElementById('publishedLink').textContent;
            navigator.clipboard?.writeText(link).then(() => {
                const btn = document.querySelector('.copy-btn');
                const originalText = btn.textContent;
                btn.textContent = '✅ Скопировано!';
                setTimeout(() => btn.textContent = originalText, 2000);
            }).catch(() => {
                const input = document.createElement('input');
                input.value = link;
                document.body.appendChild(input);
                input.select();
                document.execCommand('copy');
                document.body.removeChild(input);
                alert('Ссылка скопирована!');
            });
        }

        function openPublishedSite() {
            const link = document.getElementById('publishedLink').textContent;
            if (link) window.open(link, '_blank');
        }

        document.getElementById('publishModal').addEventListener('click', (e) => {
            if (e.target === document.getElementById('publishModal')) closePublish();
        });

        // ============================================
        //  РЕНДЕРИНГ КАНВАСА
        // ============================================
        function renderCanvas() {
            const canvas = document.getElementById('canvas');
            const emptyState = document.getElementById('emptyState');

            canvas.querySelectorAll('.canvas-element').forEach(el => el.remove());

            // Обновляем счётчик
            document.getElementById('elementCounter').textContent = `${elements.length} элементов`;

            if (elements.length === 0) {
                emptyState.style.display = 'block';
                return;
            }
            emptyState.style.display = 'none';

            const sorted = [...elements].sort((a, b) => a.order - b.order);

            sorted.forEach(el => {
                const div = document.createElement('div');
                div.className = 'canvas-element';
                if (selectedId === el.id) div.classList.add('selected');
                div.dataset.id = el.id;
                div.dataset.type = el.type;

                const delBtn = document.createElement('button');
                delBtn.className = 'delete-btn';
                delBtn.textContent = '×';
                delBtn.onclick = (e) => {
                    e.stopPropagation();
                    deleteElement(el.id);
                };
                div.appendChild(delBtn);

                div.innerHTML += getElementContent(el);

                if (el.style) {
                    if (el.style.color) div.style.color = el.style.color;
                    if (el.style.fontSize) div.style.fontSize = el.style.fontSize;
                    if (el.style.textAlign) div.style.textAlign = el.style.textAlign;
                    if (el.style.background && el.style.background !== 'transparent') {
                        div.style.background = el.style.background;
                    }
                }

                div.draggable = true;
                div.addEventListener('dragstart', (e) => {
                    e.dataTransfer.setData('text/plain', el.id);
                    e.dataTransfer.effectAllowed = 'move';
                });
                div.addEventListener('dragover', (e) => e.preventDefault());
                div.addEventListener('drop', (e) => {
                    e.preventDefault();
                    const draggedId = parseInt(e.dataTransfer.getData('text/plain'));
                    if (draggedId === el.id) return;
                    reorderElements(draggedId, el.id);
                });

                div.addEventListener('click', () => selectElement(el.id));

                canvas.appendChild(div);
            });

            if (selectedId) {
                const el = elements.find(e => e.id === selectedId);
                if (el) {
                    document.getElementById('propertiesPanel').classList.add('active');
                    document.getElementById('propText').value = el.content || '';
                    document.getElementById('propColor').value = el.style?.color || '#1f2937';
                    document.getElementById('colorValue').textContent = el.style?.color || '#1f2937';
                    document.getElementById('propSize').value = el.style?.fontSize ? parseInt(el.style.fontSize) : 16;
                    document.getElementById('propAlign').value = el.style?.textAlign || 'left';
                    document.getElementById('propBg').value = el.style?.background || '#ffffff';
                }
            } else {
                document.getElementById('propertiesPanel').classList.remove('active');
            }

            saveLocal();
        }

        function getElementContent(el) {
            const content = el.content || '';
            switch (el.type) {
                case 'heading':
                    return `<h1>${content}</h1>`;
                case 'subheading':
                    return `<h2>${content}</h2>`;
                case 'text':
                    return `<p>${content}</p>`;
                case 'button':
                    return `<button style="background:#1f6feb;color:white;padding:12px 30px;border:none;border-radius:8px;font-weight:600;cursor:pointer;">${content}</button>`;
                case 'image-placeholder':
                    return `<img src="${content}" alt="Изображение" style="max-width:100%;border-radius:8px;">`;
                case 'divider':
                    return `<hr style="border:none;border-top:2px solid #e5e7eb;margin:20px 0;">`;
                case 'input':
                    return `<input type="text" placeholder="${content}" style="width:100%;padding:12px 16px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                case 'textarea':
                    return `<textarea placeholder="${content}" style="width:100%;padding:12px 16px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;min-height:100px;resize:vertical;font-family:inherit;"></textarea>`;
                case 'card':
                    return `<div style="background:#f9fafb;border:1px solid #e5e7eb;padding:20px;border-radius:12px;">${content}</div>`;
                default:
                    return `<div>${content}</div>`;
            }
        }

        // ============================================
        //  УПРАВЛЕНИЕ ЭЛЕМЕНТАМИ
        // ============================================
        function addElement(type, content, order) {
            const el = {
                id: ++elementIdCounter,
                type: type,
                content: content || '',
                order: order || elements.length,
                style: {
                    color: '#1f2937',
                    fontSize: '16px',
                    textAlign: 'left',
                    background: 'transparent'
                }
            };
            elements.push(el);
            renderCanvas();
            selectElement(el.id);

            // Скроллим к новому элементу
            setTimeout(() => {
                const canvasWrapper = document.getElementById('canvasWrapper');
                canvasWrapper.scrollTop = canvasWrapper.scrollHeight;
            }, 50);
        }

        function deleteElement(id) {
            elements = elements.filter(e => e.id !== id);
            if (selectedId === id) selectedId = null;
            renderCanvas();
        }

        function deleteSelected() {
            if (selectedId) deleteElement(selectedId);
        }

        function selectElement(id) {
            selectedId = id;
            renderCanvas();
        }

        function updateSelectedElement(prop, value) {
            if (!selectedId) return;
            const el = elements.find(e => e.id === selectedId);
            if (!el) return;

            if (prop === 'text') {
                el.content = value;
            } else if (prop === 'color') {
                if (!el.style) el.style = {};
                el.style.color = value;
                document.getElementById('colorValue').textContent = value;
            } else if (prop === 'size') {
                if (!el.style) el.style = {};
                el.style.fontSize = value;
            } else if (prop === 'align') {
                if (!el.style) el.style = {};
                el.style.textAlign = value;
            } else if (prop === 'bg') {
                if (!el.style) el.style = {};
                el.style.background = value;
            }
            renderCanvas();
        }

        function reorderElements(draggedId, targetId) {
            const draggedIndex = elements.findIndex(e => e.id === draggedId);
            const targetIndex = elements.findIndex(e => e.id === targetId);
            if (draggedIndex === -1 || targetIndex === -1) return;

            const [dragged] = elements.splice(draggedIndex, 1);
            elements.splice(targetIndex, 0, dragged);
            elements.forEach((e, i) => e.order = i);
            renderCanvas();
        }

        function clearCanvas() {
            if (elements.length === 0) return;
            if (confirm('Удалить все элементы?')) {
                elements = [];
                selectedId = null;
                renderCanvas();
            }
        }

        // ============================================
        //  ЛОКАЛЬНОЕ СОХРАНЕНИЕ
        // ============================================
        function saveLocal() {
            try {
                localStorage.setItem('sitecraft_elements', JSON.stringify(elements));
                localStorage.setItem('sitecraft_counter', String(elementIdCounter));
            } catch (e) {}
        }

        function loadLocal() {
            try {
                const saved = localStorage.getItem('sitecraft_elements');
                if (saved) {
                    elements = JSON.parse(saved);
                    elementIdCounter = parseInt(localStorage.getItem('sitecraft_counter')) || 0;
                    renderCanvas();
                    return true;
                }
            } catch (e) {}
            return false;
        }

        // ============================================
        //  DRAG & DROP
        // ============================================
        document.querySelectorAll('.element-item').forEach(item => {
            item.addEventListener('dragstart', (e) => {
                e.dataTransfer.setData('text/plain', JSON.stringify({
                    type: item.dataset.type,
                    content: item.dataset.content
                }));
                e.dataTransfer.effectAllowed = 'copy';
            });
        });

        const canvas = document.getElementById('canvas');
        const canvasWrapper = document.getElementById('canvasWrapper');

        canvas.addEventListener('dragover', (e) => e.preventDefault());

        canvas.addEventListener('drop', (e) => {
            e.preventDefault();
            const data = e.dataTransfer.getData('text/plain');
            if (!data) return;
            try {
                const parsed = JSON.parse(data);
                addElement(parsed.type, parsed.content);
            } catch (err) {}
        });

        canvas.addEventListener('click', (e) => {
            if (e.target === canvas || e.target === document.getElementById('emptyState')) {
                selectedId = null;
                renderCanvas();
            }
        });

        // ============================================
        //  ЭКСПОРТ
        // ============================================
        function exportHTML() {
            const html = generateHTML();
            const blob = new Blob([html], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `site-${Date.now()}.html`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // ============================================
        //  ИНИЦИАЛИЗАЦИЯ
        // ============================================
        if (!loadLocal()) {
            setTimeout(() => {
                addElement('heading', 'Добро пожаловать в SiteCraft!');
                addElement('text', 'Создайте свой первый сайт за 5 минут. Перетаскивайте элементы и редактируйте их.');
                addElement('button', 'Начать');
                addElement('divider', '');
                addElement('card', '✨ Это карточка. Вы можете добавить сюда любой контент.');
                addElement('input', 'Введите ваш email');
                addElement('textarea', 'Ваше сообщение...');
                selectedId = null;
                renderCanvas();
            }, 300);
        }

        console.log('🚀 SiteCraft загружен!');
        console.log(`📁 Элементов: ${elements.length}`);
        console.log('🔑 Для публикации нужен GitHub токен');
        console.log('📜 Скролл работает! Добавляйте элементы и листайте вниз.');
    </script>
</body>
</html>

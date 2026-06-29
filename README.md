<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SiteCraft PRO — Конструктор сайтов</title>
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

        /* Режим просмотра сайта (скрываем всё лишнее) */
        body.view-mode .topbar {
            display: none !important;
        }
        body.view-mode .sidebar {
            display: none !important;
        }
        body.view-mode .properties-panel {
            display: none !important;
        }
        body.view-mode .canvas-wrapper {
            padding: 0 !important;
            background: #ffffff !important;
        }
        body.view-mode .canvas {
            box-shadow: none !important;
            border-radius: 0 !important;
            min-height: 100vh !important;
            padding: 40px 50px !important;
            margin: 0 !important;
            max-width: 100% !important;
        }
        body.view-mode .canvas .empty-state {
            display: none !important;
        }
        body.view-mode .canvas-element {
            cursor: default !important;
        }
        body.view-mode .canvas-element:hover {
            border-color: transparent !important;
            background: transparent !important;
        }
        body.view-mode .canvas-element .delete-btn {
            display: none !important;
        }
        body.view-mode .canvas-element.selected {
            border-color: transparent !important;
            background: transparent !important;
            box-shadow: none !important;
        }

        /* ===== ВЕРХНЯЯ ПАНЕЛЬ ===== */
        .topbar {
            background: #161b22;
            border-bottom: 1px solid #30363d;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 8px;
            z-index: 10;
            flex-shrink: 0;
        }

        .topbar .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 20px;
            font-weight: 700;
            background: linear-gradient(135deg, #58a6ff, #3fb950);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .topbar .actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 6px 16px;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            font-size: 13px;
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

        /* ===== ОСНОВНАЯ ОБЛАСТЬ ===== */
        .main {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        /* ===== БОКОВАЯ ПАНЕЛЬ ===== */
        .sidebar {
            width: 280px;
            background: #161b22;
            border-right: 1px solid #30363d;
            padding: 12px;
            overflow-y: auto;
            flex-shrink: 0;
        }

        .sidebar::-webkit-scrollbar {
            width: 6px;
        }
        .sidebar::-webkit-scrollbar-track {
            background: #0d1117;
        }
        .sidebar::-webkit-scrollbar-thumb {
            background: #30363d;
            border-radius: 3px;
        }

        .sidebar h3 {
            font-size: 11px;
            color: #8b949e;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin: 10px 0 6px;
        }

        .sidebar h3:first-child {
            margin-top: 0;
        }

        .element-list {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 5px;
        }

        .element-item {
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 6px;
            padding: 8px 4px;
            text-align: center;
            cursor: grab;
            transition: all 0.2s;
            font-size: 11px;
            user-select: none;
        }

        .element-item:hover {
            border-color: #58a6ff;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(88, 166, 255, 0.15);
        }

        .element-item .icon {
            font-size: 20px;
            display: block;
            margin-bottom: 2px;
        }

        /* ===== РАБОЧАЯ ОБЛАСТЬ (ЗДЕСЬ СКРОЛЛ!) ===== */
        .canvas-wrapper {
            flex: 1;
            padding: 20px;
            overflow-y: auto; /* ← ГЛАВНЫЙ СКРОЛЛ */
            background: #0d1117;
            height: 100%;
            /* Для Firefox */
            scrollbar-width: thin;
            scrollbar-color: #30363d #0d1117;
        }

        /* Стили для скролла в Chrome/Edge/Safari */
        .canvas-wrapper::-webkit-scrollbar {
            width: 10px;
            height: 10px;
        }
        .canvas-wrapper::-webkit-scrollbar-track {
            background: #0d1117;
            border-radius: 5px;
        }
        .canvas-wrapper::-webkit-scrollbar-thumb {
            background: #30363d;
            border-radius: 5px;
            transition: all 0.2s;
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
            padding: 30px 40px;
            position: relative;
            transition: all 0.2s;
        }

        .canvas .empty-state {
            text-align: center;
            color: #9ca3af;
            padding: 60px 20px;
            font-size: 16px;
        }

        .canvas .empty-state .big {
            font-size: 48px;
            display: block;
            margin-bottom: 15px;
        }

        /* ===== ЭЛЕМЕНТЫ В КАНВАСЕ ===== */
        .canvas-element {
            position: relative;
            margin: 6px 0;
            padding: 6px 10px;
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
            top: -8px;
            right: -8px;
            background: #da3633;
            color: white;
            border: none;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            font-size: 12px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            line-height: 1;
        }

        .canvas-element:hover .delete-btn {
            display: flex;
        }

        /* Стили элементов */
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
        .canvas-element[data-type="small-text"] {
            font-size: 13px;
            line-height: 1.5;
            color: #6b7280;
        }
        .canvas-element[data-type="button"] {
            display: inline-block;
            background: #1f6feb;
            color: white !important;
            padding: 10px 28px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            border: none;
        }
        .canvas-element[data-type="button"]:hover {
            background: #388bfd;
        }
        .canvas-element[data-type="button-outline"] {
            display: inline-block;
            background: transparent;
            color: #1f6feb !important;
            padding: 10px 28px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            border: 2px solid #1f6feb;
        }
        .canvas-element[data-type="button-outline"]:hover {
            background: #1f6feb;
            color: white !important;
        }
        .canvas-element[data-type="image-placeholder"] {
            background: #f3f4f6;
            padding: 30px;
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
            margin: 15px 0;
        }
        .canvas-element[data-type="divider-dashed"] {
            border: none;
            border-top: 2px dashed #e5e7eb;
            padding: 0;
            height: 2px;
            margin: 15px 0;
        }
        .canvas-element[data-type="divider-dotted"] {
            border: none;
            border-top: 2px dotted #e5e7eb;
            padding: 0;
            height: 2px;
            margin: 15px 0;
        }
        .canvas-element[data-type="input"] input {
            width: 100%;
            padding: 10px 14px;
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
            padding: 10px 14px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
            min-height: 80px;
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
        .canvas-element[data-type="card-shadow"] {
            background: #ffffff;
            border: 1px solid #e5e7eb;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        .canvas-element[data-type="card-colored"] {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white !important;
            padding: 20px;
            border-radius: 12px;
        }
        .canvas-element[data-type="list"] ul {
            padding-left: 20px;
            line-height: 1.8;
        }
        .canvas-element[data-type="list"] ul li {
            list-style-type: disc;
        }
        .canvas-element[data-type="list-number"] ol {
            padding-left: 20px;
            line-height: 1.8;
        }
        .canvas-element[data-type="list-number"] ol li {
            list-style-type: decimal;
        }
        .canvas-element[data-type="quote"] {
            background: #f3f4f6;
            border-left: 4px solid #1f6feb;
            padding: 15px 20px;
            border-radius: 4px;
            font-style: italic;
            font-size: 18px;
            color: #374151;
        }
        .canvas-element[data-type="badge"] {
            display: inline-block;
            background: #1f6feb;
            color: white !important;
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }
        .canvas-element[data-type="badge-success"] {
            display: inline-block;
            background: #238636;
            color: white !important;
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }
        .canvas-element[data-type="badge-danger"] {
            display: inline-block;
            background: #da3633;
            color: white !important;
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }
        .canvas-element[data-type="badge-warning"] {
            display: inline-block;
            background: #d29922;
            color: #0a0e17 !important;
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }
        .canvas-element[data-type="progress"] {
            width: 100%;
            height: 8px;
            background: #e5e7eb;
            border-radius: 4px;
            overflow: hidden;
        }
        .canvas-element[data-type="progress"] .fill {
            height: 100%;
            background: #1f6feb;
            border-radius: 4px;
            width: 70%;
        }
        .canvas-element[data-type="progress-success"] {
            width: 100%;
            height: 8px;
            background: #e5e7eb;
            border-radius: 4px;
            overflow: hidden;
        }
        .canvas-element[data-type="progress-success"] .fill {
            height: 100%;
            background: #238636;
            border-radius: 4px;
            width: 45%;
        }
        .canvas-element[data-type="alert"] {
            padding: 12px 16px;
            border-radius: 8px;
            border: 1px solid #e5e7eb;
            background: #f3f4f6;
        }
        .canvas-element[data-type="alert-success"] {
            padding: 12px 16px;
            border-radius: 8px;
            border: 1px solid #238636;
            background: rgba(35, 134, 54, 0.1);
            color: #238636;
        }
        .canvas-element[data-type="alert-danger"] {
            padding: 12px 16px;
            border-radius: 8px;
            border: 1px solid #da3633;
            background: rgba(218, 54, 51, 0.1);
            color: #da3633;
        }
        .canvas-element[data-type="alert-warning"] {
            padding: 12px 16px;
            border-radius: 8px;
            border: 1px solid #d29922;
            background: rgba(210, 153, 34, 0.1);
            color: #d29922;
        }
        .canvas-element[data-type="table"] table {
            width: 100%;
            border-collapse: collapse;
        }
        .canvas-element[data-type="table"] th {
            background: #f3f4f6;
            padding: 10px 12px;
            text-align: left;
            border: 1px solid #e5e7eb;
            font-weight: 600;
        }
        .canvas-element[data-type="table"] td {
            padding: 8px 12px;
            border: 1px solid #e5e7eb;
        }
        .canvas-element[data-type="video"] {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: 8px;
            background: #0a0e17;
        }
        .canvas-element[data-type="video"] iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        .canvas-element[data-type="gallery"] {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 8px;
        }
        .canvas-element[data-type="gallery"] img {
            width: 100%;
            height: 100px;
            object-fit: cover;
            border-radius: 6px;
        }
        .canvas-element[data-type="checkbox"] {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .canvas-element[data-type="checkbox"] input[type="checkbox"] {
            width: 18px;
            height: 18px;
            accent-color: #1f6feb;
        }
        .canvas-element[data-type="radio"] {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .canvas-element[data-type="radio"] input[type="radio"] {
            width: 18px;
            height: 18px;
            accent-color: #1f6feb;
        }
        .canvas-element[data-type="select"] select {
            width: 100%;
            padding: 10px 14px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
            background: white;
        }
        .canvas-element[data-type="select"] select:focus {
            outline: none;
            border-color: #1f6feb;
        }
        .canvas-element[data-type="date"] input[type="date"] {
            width: 100%;
            padding: 10px 14px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 16px;
        }
        .canvas-element[data-type="date"] input[type="date"]:focus {
            outline: none;
            border-color: #1f6feb;
        }
        .canvas-element[data-type="color"] input[type="color"] {
            width: 50px;
            height: 50px;
            padding: 2px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            cursor: pointer;
        }
        .canvas-element[data-type="range"] input[type="range"] {
            width: 100%;
            accent-color: #1f6feb;
        }
        .canvas-element[data-type="tag"] {
            display: inline-block;
            background: #e5e7eb;
            color: #1f2937;
            padding: 4px 12px;
            border-radius: 4px;
            font-size: 13px;
            margin: 2px;
        }
        .canvas-element[data-type="tag-blue"] {
            display: inline-block;
            background: #dbeafe;
            color: #1f6feb;
            padding: 4px 12px;
            border-radius: 4px;
            font-size: 13px;
            margin: 2px;
        }
        .canvas-element[data-type="tag-green"] {
            display: inline-block;
            background: #d1fae5;
            color: #238636;
            padding: 4px 12px;
            border-radius: 4px;
            font-size: 13px;
            margin: 2px;
        }

        /* ===== ПАНЕЛЬ СВОЙСТВ ===== */
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
            margin-bottom: 12px;
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

        .prop-group .link-input {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .prop-group .link-input input {
            flex: 1;
        }

        .prop-group .link-input .btn-small {
            padding: 8px 12px;
            background: #21262d;
            border: 1px solid #30363d;
            border-radius: 6px;
            color: #e6edf3;
            cursor: pointer;
            font-size: 12px;
            white-space: nowrap;
        }

        .prop-group .link-input .btn-small:hover {
            background: #30363d;
        }

        .element-counter {
            background: #21262d;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 13px;
            color: #8b949e;
            margin-left: 10px;
        }

        /* ===== МОДАЛКА ПРОСМОТРА ===== */
        .view-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #ffffff;
            z-index: 9999;
            overflow-y: auto;
            padding: 40px 20px;
        }

        .view-modal.active {
            display: block;
        }

        .view-modal .close-view {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #161b22;
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            font-size: 20px;
            cursor: pointer;
            z-index: 10000;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }

        .view-modal .close-view:hover {
            background: #30363d;
        }

        .view-modal .site-content {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            color: #1f2937;
        }

        /* ===== АДАПТИВ ===== */
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
                grid-template-columns: 1fr 1fr;
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
                max-height: 200px;
            }
            .properties-panel {
                width: 100%;
                border-left: none;
                border-top: 1px solid #30363d;
            }
            .topbar .actions .btn {
                font-size: 11px;
                padding: 5px 10px;
            }
            .element-list {
                grid-template-columns: 1fr 1fr 1fr;
            }
            .view-modal {
                padding: 20px 10px;
            }
            .view-modal .close-view {
                top: 10px;
                right: 10px;
                width: 32px;
                height: 32px;
                font-size: 16px;
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
    </style>
</head>
<body>
    <!-- ===== ВЕРХНЯЯ ПАНЕЛЬ ===== -->
    <div class="topbar">
        <div class="logo">🚀 SiteCraft PRO</div>
        <div class="actions">
            <span class="element-counter" id="elementCounter">0 элементов</span>
            <button class="btn btn-outline" onclick="clearCanvas()">🗑 Очистить</button>
            <button class="btn btn-publish" onclick="publishSite()">🌐 Хостинг</button>
            <button class="btn btn-success" onclick="exportHTML()">💾 Скачать</button>
        </div>
    </div>

    <!-- ===== ОСНОВНАЯ ОБЛАСТЬ ===== -->
    <div class="main">
        <!-- Боковая панель -->
        <div class="sidebar">
            <h3>📝 Текст</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="heading" data-content="Заголовок H1">
                    <span class="icon">📰</span> H1
                </div>
                <div class="element-item" draggable="true" data-type="subheading" data-content="Подзаголовок H2">
                    <span class="icon">📝</span> H2
                </div>
                <div class="element-item" draggable="true" data-type="text" data-content="Текст абзаца...">
                    <span class="icon">📄</span> Текст
                </div>
                <div class="element-item" draggable="true" data-type="small-text" data-content="Маленький текст...">
                    <span class="icon">🔤</span> Мелкий
                </div>
                <div class="element-item" draggable="true" data-type="quote" data-content="Цитата">
                    <span class="icon">💬</span> Цитата
                </div>
            </div>

            <h3>🔘 Кнопки</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="button" data-content="Кнопка" data-link="https://example.com">
                    <span class="icon">🔵</span> Кнопка
                </div>
                <div class="element-item" draggable="true" data-type="button-outline" data-content="Кнопка" data-link="#">
                    <span class="icon">⬜</span> Обводка
                </div>
            </div>

            <h3>🏷️ Бейджи</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="badge" data-content="Новинка">
                    <span class="icon">🔵</span> Бейдж
                </div>
                <div class="element-item" draggable="true" data-type="badge-success" data-content="Успешно">
                    <span class="icon">🟢</span> Успех
                </div>
                <div class="element-item" draggable="true" data-type="badge-danger" data-content="Ошибка">
                    <span class="icon">🔴</span> Ошибка
                </div>
                <div class="element-item" draggable="true" data-type="badge-warning" data-content="Внимание">
                    <span class="icon">🟡</span> Внимание
                </div>
            </div>

            <h3>📦 Контейнеры</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="card" data-content="Карточка">
                    <span class="icon">📇</span> Карточка
                </div>
                <div class="element-item" draggable="true" data-type="card-shadow" data-content="С тенью">
                    <span class="icon">🌓</span> Тень
                </div>
                <div class="element-item" draggable="true" data-type="card-colored" data-content="Цветная">
                    <span class="icon">🌈</span> Цветная
                </div>
            </div>

            <h3>📋 Списки</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="list" data-content="Пункт 1\nПункт 2\nПункт 3">
                    <span class="icon">•</span> Маркер
                </div>
                <div class="element-item" draggable="true" data-type="list-number" data-content="1. Первый\n2. Второй\n3. Третий">
                    <span class="icon">1.</span> Нумер.
                </div>
            </div>

            <h3>⚡ Прогресс</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="progress" data-content="">
                    <span class="icon">📊</span> Прогресс
                </div>
                <div class="element-item" draggable="true" data-type="progress-success" data-content="">
                    <span class="icon">✅</span> Успех
                </div>
            </div>

            <h3>⚠️ Алerts</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="alert" data-content="Информация">
                    <span class="icon">ℹ️</span> Инфо
                </div>
                <div class="element-item" draggable="true" data-type="alert-success" data-content="Успешно!">
                    <span class="icon">✅</span> Успех
                </div>
                <div class="element-item" draggable="true" data-type="alert-danger" data-content="Ошибка!">
                    <span class="icon">❌</span> Ошибка
                </div>
                <div class="element-item" draggable="true" data-type="alert-warning" data-content="Внимание!">
                    <span class="icon">⚠️</span> Внимание
                </div>
            </div>

            <h3>🖼️ Медиа</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="image-placeholder" data-content="https://via.placeholder.com/600x300">
                    <span class="icon">🖼️</span> Картинка
                </div>
                <div class="element-item" draggable="true" data-type="video" data-content="https://www.youtube.com/embed/dQw4w9WgXcQ">
                    <span class="icon">▶️</span> Видео
                </div>
                <div class="element-item" draggable="true" data-type="gallery" data-content="https://via.placeholder.com/150/1f6feb/fff">
                    <span class="icon">🖼️</span> Галерея
                </div>
            </div>

            <h3>➖ Разделители</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="divider" data-content="">
                    <span class="icon">➖</span> Сплошной
                </div>
                <div class="element-item" draggable="true" data-type="divider-dashed" data-content="">
                    <span class="icon">╌</span> Пунктир
                </div>
                <div class="element-item" draggable="true" data-type="divider-dotted" data-content="">
                    <span class="icon">┈</span> Точки
                </div>
            </div>

            <h3>📊 Формы</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="input" data-content="Введите текст...">
                    <span class="icon">✏️</span> Поле
                </div>
                <div class="element-item" draggable="true" data-type="textarea" data-content="Введите текст...">
                    <span class="icon">📋</span> Текст
                </div>
                <div class="element-item" draggable="true" data-type="select" data-content="Выберите вариант">
                    <span class="icon">📌</span> Выбор
                </div>
                <div class="element-item" draggable="true" data-type="date" data-content="">
                    <span class="icon">📅</span> Дата
                </div>
                <div class="element-item" draggable="true" data-type="color" data-content="">
                    <span class="icon">🎨</span> Цвет
                </div>
                <div class="element-item" draggable="true" data-type="range" data-content="">
                    <span class="icon">🎚️</span> Слайдер
                </div>
                <div class="element-item" draggable="true" data-type="checkbox" data-content="Чекбокс">
                    <span class="icon">☑️</span> Чекбокс
                </div>
                <div class="element-item" draggable="true" data-type="radio" data-content="Радио">
                    <span class="icon">⭕</span> Радио
                </div>
            </div>

            <h3>🏷️ Теги</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="tag" data-content="Тег">
                    <span class="icon">🏷️</span> Тег
                </div>
                <div class="element-item" draggable="true" data-type="tag-blue" data-content="Синий">
                    <span class="icon">🔵</span> Синий
                </div>
                <div class="element-item" draggable="true" data-type="tag-green" data-content="Зеленый">
                    <span class="icon">🟢</span> Зеленый
                </div>
            </div>

            <h3>📊 Таблица</h3>
            <div class="element-list">
                <div class="element-item" draggable="true" data-type="table" data-content="Имя|Возраст\nАнна|25\nМакс|30">
                    <span class="icon">📊</span> Таблица
                </div>
            </div>
        </div>

        <!-- ===== РАБОЧАЯ ОБЛАСТЬ С СКРОЛЛОМ ===== -->
        <div class="canvas-wrapper" id="canvasWrapper">
            <div class="canvas" id="canvas">
                <div class="empty-state" id="emptyState">
                    <span class="big">🎨</span>
                    Перетащи элемент с панели слева<br>
                    или кликни на элемент для редактирования
                </div>
            </div>
        </div>

        <!-- Панель свойств -->
        <div class="properties-panel" id="propertiesPanel">
            <h3>⚙️ Свойства</h3>
            <div class="prop-group">
                <label>Текст</label>
                <input type="text" id="propText" onchange="updateSelectedElement('text', this.value)">
            </div>
            <div class="prop-group" id="linkGroup" style="display:none;">
                <label>🔗 Ссылка (для кнопки)</label>
                <div class="link-input">
                    <input type="url" id="propLink" placeholder="https://example.com" onchange="updateSelectedElement('link', this.value)">
                    <button class="btn-small" onclick="document.getElementById('propLink').value='https://'; updateSelectedElement('link', document.getElementById('propLink').value);">🔄</button>
                </div>
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

    <!-- Модалка просмотра -->
    <div class="view-modal" id="viewModal">
        <button class="close-view" onclick="closeViewMode()">✕</button>
        <div class="site-content" id="viewContent"></div>
    </div>

    <script>
        // ============================================
        //  СОСТОЯНИЕ
        // ============================================
        let elements = [];
        let selectedId = null;
        let elementIdCounter = 0;
        let publishedUrl = '';
        let siteId = '';

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
                    case 'small-text':
                        return `<p${styleAttr} style="font-size:13px;color:#6b7280;">${el.content}</p>`;
                    case 'button': {
                        const link = el.link || '#';
                        const target = link.startsWith('http') ? ' target="_blank"' : '';
                        return `<a href="${link}"${target} style="text-decoration:none;"><button style="background:#1f6feb;color:white;padding:10px 28px;border:none;border-radius:8px;font-weight:600;cursor:pointer;${style}">${el.content}</button></a>`;
                    }
                    case 'button-outline': {
                        const link = el.link || '#';
                        const target = link.startsWith('http') ? ' target="_blank"' : '';
                        return `<a href="${link}"${target} style="text-decoration:none;"><button style="background:transparent;color:#1f6feb;padding:10px 28px;border:2px solid #1f6feb;border-radius:8px;font-weight:600;cursor:pointer;${style}">${el.content}</button></a>`;
                    }
                    case 'image-placeholder':
                        return `<img src="${el.content}" alt="Image" style="max-width:100%;border-radius:8px;">`;
                    case 'divider':
                        return `<hr style="border:none;border-top:2px solid #e5e7eb;margin:15px 0;">`;
                    case 'divider-dashed':
                        return `<hr style="border:none;border-top:2px dashed #e5e7eb;margin:15px 0;">`;
                    case 'divider-dotted':
                        return `<hr style="border:none;border-top:2px dotted #e5e7eb;margin:15px 0;">`;
                    case 'input':
                        return `<input type="text" placeholder="${el.content}" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                    case 'textarea':
                        return `<textarea placeholder="${el.content}" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;min-height:80px;resize:vertical;font-family:inherit;"></textarea>`;
                    case 'card':
                        return `<div style="background:#f9fafb;border:1px solid #e5e7eb;padding:20px;border-radius:12px;">${el.content}</div>`;
                    case 'card-shadow':
                        return `<div style="background:#ffffff;border:1px solid #e5e7eb;padding:20px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.08);">${el.content}</div>`;
                    case 'card-colored':
                        return `<div style="background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;padding:20px;border-radius:12px;">${el.content}</div>`;
                    case 'list': {
                        const items = el.content.split('\n').filter(s => s.trim());
                        return `<ul style="padding-left:20px;line-height:1.8;">${items.map(i => `<li>${i}</li>`).join('')}</ul>`;
                    }
                    case 'list-number': {
                        const items = el.content.split('\n').filter(s => s.trim());
                        return `<ol style="padding-left:20px;line-height:1.8;">${items.map(i => `<li>${i}</li>`).join('')}</ol>`;
                    }
                    case 'quote':
                        return `<blockquote style="background:#f3f4f6;border-left:4px solid #1f6feb;padding:15px 20px;border-radius:4px;font-style:italic;font-size:18px;color:#374151;">${el.content}</blockquote>`;
                    case 'badge':
                        return `<span style="display:inline-block;background:#1f6feb;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${el.content}</span>`;
                    case 'badge-success':
                        return `<span style="display:inline-block;background:#238636;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${el.content}</span>`;
                    case 'badge-danger':
                        return `<span style="display:inline-block;background:#da3633;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${el.content}</span>`;
                    case 'badge-warning':
                        return `<span style="display:inline-block;background:#d29922;color:#0a0e17;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${el.content}</span>`;
                    case 'progress':
                        return `<div style="width:100%;height:8px;background:#e5e7eb;border-radius:4px;overflow:hidden;"><div style="height:100%;background:#1f6feb;border-radius:4px;width:70%;"></div></div>`;
                    case 'progress-success':
                        return `<div style="width:100%;height:8px;background:#e5e7eb;border-radius:4px;overflow:hidden;"><div style="height:100%;background:#238636;border-radius:4px;width:45%;"></div></div>`;
                    case 'alert':
                        return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #e5e7eb;background:#f3f4f6;">${el.content}</div>`;
                    case 'alert-success':
                        return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #238636;background:rgba(35,134,54,0.1);color:#238636;">${el.content}</div>`;
                    case 'alert-danger':
                        return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #da3633;background:rgba(218,54,51,0.1);color:#da3633;">${el.content}</div>`;
                    case 'alert-warning':
                        return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #d29922;background:rgba(210,153,34,0.1);color:#d29922;">${el.content}</div>`;
                    case 'table': {
                        const rows = el.content.split('\n').filter(s => s.trim());
                        if (rows.length === 0) return '';
                        const header = rows[0].split('|');
                        const data = rows.slice(1).map(r => r.split('|'));
                        let table = `<table style="width:100%;border-collapse:collapse;"><thead><tr>`;
                        header.forEach(h => {
                            table +=
                                `<th style="background:#f3f4f6;padding:10px 12px;text-align:left;border:1px solid #e5e7eb;font-weight:600;">${h.trim()}</th>`;
                        });
                        table += `</tr></thead><tbody>`;
                        data.forEach(row => {
                            table += `<tr>`;
                            row.forEach(cell => {
                                table +=
                                    `<td style="padding:8px 12px;border:1px solid #e5e7eb;">${cell.trim()}</td>`;
                            });
                            table += `</tr>`;
                        });
                        table += `</tbody></table>`;
                        return table;
                    }
                    case 'video':
                        return `<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:8px;background:#0a0e17;"><iframe src="${el.content}" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" allowfullscreen></iframe></div>`;
                    case 'gallery': {
                        const images = el.content.split(',').filter(s => s.trim());
                        return `<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;">${images.map(img => `<img src="${img.trim()}" style="width:100%;height:100px;object-fit:cover;border-radius:6px;">`).join('')}</div>`;
                    }
                    case 'checkbox':
                        return `<div style="display:flex;align-items:center;gap:10px;"><input type="checkbox" style="width:18px;height:18px;accent-color:#1f6feb;"> <span>${el.content}</span></div>`;
                    case 'radio':
                        return `<div style="display:flex;align-items:center;gap:10px;"><input type="radio" name="radio" style="width:18px;height:18px;accent-color:#1f6feb;"> <span>${el.content}</span></div>`;
                    case 'select':
                        return `<select style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;background:white;"><option>${el.content}</option><option>Вариант 2</option><option>Вариант 3</option></select>`;
                    case 'date':
                        return `<input type="date" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                    case 'color':
                        return `<input type="color" style="width:50px;height:50px;padding:2px;border:2px solid #d1d5db;border-radius:8px;cursor:pointer;">`;
                    case 'range':
                        return `<input type="range" style="width:100%;accent-color:#1f6feb;">`;
                    case 'tag':
                        return `<span style="display:inline-block;background:#e5e7eb;color:#1f2937;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${el.content}</span>`;
                    case 'tag-blue':
                        return `<span style="display:inline-block;background:#dbeafe;color:#1f6feb;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${el.content}</span>`;
                    case 'tag-green':
                        return `<span style="display:inline-block;background:#d1fae5;color:#238636;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${el.content}</span>`;
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
                input, textarea, select { font-family: inherit; }
                a { text-decoration: none; }
            </style>
        </head>
        <body>
            ${bodyContent}
        </body>
        </html>`;
        }

        // ============================================
        //  ХОСТИНГ
        // ============================================
        async function publishSite() {
            try {
                const html = generateHTML();
                siteId = 'site_' + Date.now().toString(36) + '_' + Math.random().toString(36).substr(2, 6);

                const sites = JSON.parse(localStorage.getItem('sitecraft_hosted') || '{}');
                sites[siteId] = {
                    html: html,
                    created: Date.now(),
                    views: 0,
                    elements: elements.length
                };
                localStorage.setItem('sitecraft_hosted', JSON.stringify(sites));
                localStorage.setItem('sitecraft_current_site', siteId);

                publishedUrl = window.location.origin + window.location.pathname + '?site=' + siteId;
                localStorage.setItem('sitecraft_published_url', publishedUrl);
                localStorage.setItem('sitecraft_published_id', siteId);

                openViewMode(html);

                try {
                    await navigator.clipboard?.writeText(publishedUrl);
                } catch (e) {}

            } catch (error) {
                alert('Ошибка публикации: ' + error.message);
            }
        }

        // ============================================
        //  РЕЖИМ ПРОСМОТРА
        // ============================================
        function openViewMode(html) {
            const modal = document.getElementById('viewModal');
            const content = document.getElementById('viewContent');
            content.innerHTML = html;
            modal.classList.add('active');
            document.body.style.overflow = 'hidden';
        }

        function closeViewMode() {
            document.getElementById('viewModal').classList.remove('active');
            document.body.style.overflow = '';
        }

        // ============================================
        //  ПРОСМОТР ПО ССЫЛКЕ
        // ============================================
        function viewSite() {
            const params = new URLSearchParams(window.location.search);
            const siteId = params.get('site');

            if (siteId) {
                try {
                    const sites = JSON.parse(localStorage.getItem('sitecraft_hosted') || '{}');
                    const site = sites[siteId];

                    if (site) {
                        site.views = (site.views || 0) + 1;
                        sites[siteId] = site;
                        localStorage.setItem('sitecraft_hosted', JSON.stringify(sites));

                        document.body.innerHTML = '';
                        document.body.style.background = '#ffffff';
                        document.body.style.margin = '0';
                        document.body.style.padding = '0';
                        document.body.style.overflow = 'auto';
                        document.body.innerHTML = site.html;

                        try {
                            const currentSite = localStorage.getItem('sitecraft_current_site');
                            if (currentSite === siteId) {
                                const backBtn = document.createElement('div');
                                backBtn.style.cssText =
                                    'position:fixed;top:20px;right:20px;background:#161b22;color:white;padding:10px 20px;border:none;border-radius:8px;cursor:pointer;font-weight:600;z-index:9999;font-family:sans-serif;box-shadow:0 4px 12px rgba(0,0,0,0.3);';
                                backBtn.textContent = '✕ Редактировать';
                                backBtn.onclick = () => {
                                    window.location.href = window.location.pathname;
                                };
                                document.body.appendChild(backBtn);
                            }
                        } catch (e) {}

                        document.title = 'Сайт на SiteCraft';
                        return true;
                    }
                } catch (e) {}
            }
            return false;
        }

        // ============================================
        //  РЕНДЕРИНГ
        // ============================================
        function renderCanvas() {
            const canvas = document.getElementById('canvas');
            const emptyState = document.getElementById('emptyState');

            canvas.querySelectorAll('.canvas-element').forEach(el => el.remove());

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

                if (el.type === 'button' && el.link) {
                    const linkLabel = document.createElement('div');
                    linkLabel.style.cssText =
                        'font-size:10px; color:#8b949e; margin-top:4px; font-family:monospace; overflow:hidden; text-overflow:ellipsis; white-space:nowrap;';
                    linkLabel.textContent = `🔗 ${el.link}`;
                    div.appendChild(linkLabel);
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

                    const linkGroup = document.getElementById('linkGroup');
                    if (el.type === 'button' || el.type === 'button-outline') {
                        linkGroup.style.display = 'block';
                        document.getElementById('propLink').value = el.link || '';
                    } else {
                        linkGroup.style.display = 'none';
                    }
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
                case 'small-text':
                    return `<p style="font-size:13px;color:#6b7280;">${content}</p>`;
                case 'button': {
                    const link = el.link || '#';
                    return `<a href="${link}" target="_blank" style="text-decoration:none;"><button style="background:#1f6feb;color:white;padding:10px 28px;border:none;border-radius:8px;font-weight:600;cursor:pointer;">${content}</button></a>`;
                }
                case 'button-outline': {
                    const link = el.link || '#';
                    return `<a href="${link}" target="_blank" style="text-decoration:none;"><button style="background:transparent;color:#1f6feb;padding:10px 28px;border:2px solid #1f6feb;border-radius:8px;font-weight:600;cursor:pointer;">${content}</button></a>`;
                }
                case 'image-placeholder':
                    return `<img src="${content}" alt="Изображение" style="max-width:100%;border-radius:8px;">`;
                case 'divider':
                    return `<hr style="border:none;border-top:2px solid #e5e7eb;margin:15px 0;">`;
                case 'divider-dashed':
                    return `<hr style="border:none;border-top:2px dashed #e5e7eb;margin:15px 0;">`;
                case 'divider-dotted':
                    return `<hr style="border:none;border-top:2px dotted #e5e7eb;margin:15px 0;">`;
                case 'input':
                    return `<input type="text" placeholder="${content}" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                case 'textarea':
                    return `<textarea placeholder="${content}" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;min-height:80px;resize:vertical;font-family:inherit;"></textarea>`;
                case 'card':
                    return `<div style="background:#f9fafb;border:1px solid #e5e7eb;padding:20px;border-radius:12px;">${content}</div>`;
                case 'card-shadow':
                    return `<div style="background:#ffffff;border:1px solid #e5e7eb;padding:20px;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.08);">${content}</div>`;
                case 'card-colored':
                    return `<div style="background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;padding:20px;border-radius:12px;">${content}</div>`;
                case 'list': {
                    const items = content.split('\n').filter(s => s.trim());
                    return `<ul style="padding-left:20px;line-height:1.8;">${items.map(i => `<li>${i}</li>`).join('')}</ul>`;
                }
                case 'list-number': {
                    const items = content.split('\n').filter(s => s.trim());
                    return `<ol style="padding-left:20px;line-height:1.8;">${items.map(i => `<li>${i}</li>`).join('')}</ol>`;
                }
                case 'quote':
                    return `<blockquote style="background:#f3f4f6;border-left:4px solid #1f6feb;padding:15px 20px;border-radius:4px;font-style:italic;font-size:18px;color:#374151;">${content}</blockquote>`;
                case 'badge':
                    return `<span style="display:inline-block;background:#1f6feb;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${content}</span>`;
                case 'badge-success':
                    return `<span style="display:inline-block;background:#238636;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${content}</span>`;
                case 'badge-danger':
                    return `<span style="display:inline-block;background:#da3633;color:white;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${content}</span>`;
                case 'badge-warning':
                    return `<span style="display:inline-block;background:#d29922;color:#0a0e17;padding:4px 14px;border-radius:20px;font-size:14px;font-weight:600;">${content}</span>`;
                case 'progress':
                    return `<div style="width:100%;height:8px;background:#e5e7eb;border-radius:4px;overflow:hidden;"><div style="height:100%;background:#1f6feb;border-radius:4px;width:70%;"></div></div>`;
                case 'progress-success':
                    return `<div style="width:100%;height:8px;background:#e5e7eb;border-radius:4px;overflow:hidden;"><div style="height:100%;background:#238636;border-radius:4px;width:45%;"></div></div>`;
                case 'alert':
                    return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #e5e7eb;background:#f3f4f6;">${content}</div>`;
                case 'alert-success':
                    return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #238636;background:rgba(35,134,54,0.1);color:#238636;">${content}</div>`;
                case 'alert-danger':
                    return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #da3633;background:rgba(218,54,51,0.1);color:#da3633;">${content}</div>`;
                case 'alert-warning':
                    return `<div style="padding:12px 16px;border-radius:8px;border:1px solid #d29922;background:rgba(210,153,34,0.1);color:#d29922;">${content}</div>`;
                case 'table': {
                    const rows = content.split('\n').filter(s => s.trim());
                    if (rows.length === 0) return '';
                    const header = rows[0].split('|');
                    const data = rows.slice(1).map(r => r.split('|'));
                    let table = `<table style="width:100%;border-collapse:collapse;"><thead><tr>`;
                    header.forEach(h => {
                        table +=
                            `<th style="background:#f3f4f6;padding:10px 12px;text-align:left;border:1px solid #e5e7eb;font-weight:600;">${h.trim()}</th>`;
                    });
                    table += `</tr></thead><tbody>`;
                    data.forEach(row => {
                        table += `<tr>`;
                        row.forEach(cell => {
                            table +=
                                `<td style="padding:8px 12px;border:1px solid #e5e7eb;">${cell.trim()}</td>`;
                        });
                        table += `</tr>`;
                    });
                    table += `</tbody></table>`;
                    return table;
                }
                case 'video':
                    return `<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:8px;background:#0a0e17;"><iframe src="${content}" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" allowfullscreen></iframe></div>`;
                case 'gallery': {
                    const images = content.split(',').filter(s => s.trim());
                    return `<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;">${images.map(img => `<img src="${img.trim()}" style="width:100%;height:100px;object-fit:cover;border-radius:6px;">`).join('')}</div>`;
                }
                case 'checkbox':
                    return `<div style="display:flex;align-items:center;gap:10px;"><input type="checkbox" style="width:18px;height:18px;accent-color:#1f6feb;"> <span>${content}</span></div>`;
                case 'radio':
                    return `<div style="display:flex;align-items:center;gap:10px;"><input type="radio" name="radio" style="width:18px;height:18px;accent-color:#1f6feb;"> <span>${content}</span></div>`;
                case 'select':
                    return `<select style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;background:white;"><option>${content}</option><option>Вариант 2</option><option>Вариант 3</option></select>`;
                case 'date':
                    return `<input type="date" style="width:100%;padding:10px 14px;border:2px solid #d1d5db;border-radius:8px;font-size:16px;">`;
                case 'color':
                    return `<input type="color" style="width:50px;height:50px;padding:2px;border:2px solid #d1d5db;border-radius:8px;cursor:pointer;">`;
                case 'range':
                    return `<input type="range" style="width:100%;accent-color:#1f6feb;">`;
                case 'tag':
                    return `<span style="display:inline-block;background:#e5e7eb;color:#1f2937;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${content}</span>`;
                case 'tag-blue':
                    return `<span style="display:inline-block;background:#dbeafe;color:#1f6feb;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${content}</span>`;
                case 'tag-green':
                    return `<span style="display:inline-block;background:#d1fae5;color:#238636;padding:4px 12px;border-radius:4px;font-size:13px;margin:2px;">${content}</span>`;
                default:
                    return `<div>${content}</div>`;
            }
        }

        // ============================================
        //  УПРАВЛЕНИЕ ЭЛЕМЕНТАМИ
        // ============================================
        function addElement(type, content, order, link) {
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

            if ((type === 'button' || type === 'button-outline') && link) {
                el.link = link;
            }

            elements.push(el);
            renderCanvas();
            selectElement(el.id);

            setTimeout(() => {
                const wrapper = document.getElementById('canvasWrapper');
                wrapper.scrollTop = wrapper.scrollHeight;
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
            } else if (prop === 'link') {
                el.link = value;
                renderCanvas();
                return;
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
        //  СОХРАНЕНИЕ
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
                    content: item.dataset.content,
                    link: item.dataset.link || ''
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
                addElement(parsed.type, parsed.content, undefined, parsed.link);
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
        if (!viewSite()) {
            if (!loadLocal()) {
                setTimeout(() => {
                    addElement('heading', 'Добро пожаловать в SiteCraft PRO!');
                    addElement('text', 'Теперь доступно 30+ элементов для создания сайтов.');
                    addElement('button', 'Начать', undefined, 'https://example.com');
                    addElement('badge', 'Новинка');
                    addElement('divider', '');
                    addElement('card', '✨ Карточка с контентом');
                    addElement('list', 'Пункт 1\nПункт 2\nПункт 3');
                    addElement('alert-success', '✅ Успешная операция!');
                    addElement('progress', '');
                    addElement('input', 'Введите ваш email');
                    addElement('textarea', 'Ваше сообщение...');
                    selectedId = null;
                    renderCanvas();
                }, 300);
            }
        }

        console.log('🚀 SiteCraft PRO загружен!');
        console.log(`📁 Элементов: ${elements.length}`);
        console.log('🎨 Доступно 30+ элементов!');
        console.log('📜 СКРОЛЛ РАБОТАЕТ! Добавь много элементов и прокручивай вниз.');
        console.log('🔗 При открытии ссылки показывается ТОЛЬКО САЙТ!');
    </script>
</body>
</html>

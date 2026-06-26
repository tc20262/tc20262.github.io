<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SiteBuilder Pro — Конструктор сайтов</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: #f0f2f5;
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* ===== ВЕРХНЯЯ ПАНЕЛЬ ===== */
        .toolbar {
            background: #fff;
            border-bottom: 1px solid #d0d7de;
            padding: 10px 20px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 10px;
            flex-shrink: 0;
            box-shadow: 0 1px 4px rgba(0,0,0,0.04);
            z-index: 10;
        }

        .toolbar .brand {
            font-weight: 700;
            font-size: 18px;
            color: #0a7cff;
            margin-right: 16px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .toolbar .brand small {
            font-weight: 400;
            font-size: 12px;
            color: #6c7a8a;
        }

        .toolbar-group {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 6px;
            margin-right: 8px;
        }

        .toolbar-group .btn {
            background: #f1f4f8;
            border: 1px solid #d0d7de;
            border-radius: 8px;
            padding: 6px 14px;
            font-size: 13px;
            font-weight: 500;
            color: #1a1a1a;
            cursor: pointer;
            transition: 0.15s;
            display: flex;
            align-items: center;
            gap: 5px;
            white-space: nowrap;
        }

        .toolbar-group .btn:hover {
            background: #e4e9f0;
            border-color: #b0b8c0;
        }

        .toolbar-group .btn.primary {
            background: #0a7cff;
            border-color: #0a7cff;
            color: #fff;
        }

        .toolbar-group .btn.primary:hover {
            background: #0066e0;
            border-color: #0066e0;
        }

        .toolbar-group .btn.success {
            background: #2b9c4c;
            border-color: #2b9c4c;
            color: #fff;
        }

        .toolbar-group .btn.success:hover {
            background: #1f7a3a;
            border-color: #1f7a3a;
        }

        .toolbar-group .btn.purple {
            background: #7c3aed;
            border-color: #7c3aed;
            color: #fff;
        }

        .toolbar-group .btn.purple:hover {
            background: #6d28d9;
            border-color: #6d28d9;
        }

        .toolbar-group .btn.add-element {
            background: #0a7cff;
            color: #fff;
            border-color: #0a7cff;
            padding: 6px 16px;
            font-weight: 600;
        }

        .toolbar-group .btn.add-element:hover {
            background: #0066e0;
            border-color: #0066e0;
        }

        .separator {
            width: 1px;
            height: 28px;
            background: #d0d7de;
            margin: 0 6px;
        }

        /* ===== ОСНОВНАЯ ОБЛАСТЬ ===== */
        .main-area {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        /* ===== ХОЛСТ ===== */
        .canvas-wrapper {
            flex: 1;
            padding: 20px;
            overflow: auto;
            background: #e8edf2;
            display: flex;
            justify-content: center;
            align-items: flex-start;
        }

        #siteCanvas {
            width: 100%;
            max-width: 1000px;
            min-height: 600px;
            background: #ffffff;
            border-radius: 12px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.08);
            padding: 30px;
            position: relative;
            transition: 0.1s;
        }

        /* ===== СТИЛИ ДЛЯ ЭЛЕМЕНТОВ ===== */
        .canvas-element {
            position: relative;
            margin: 6px 0;
            padding: 10px 14px;
            border: 2px solid transparent;
            border-radius: 8px;
            cursor: move;
            transition: border-color 0.15s, box-shadow 0.15s;
            min-height: 30px;
        }

        .canvas-element:hover {
            border-color: #c8d0d8;
        }

        .canvas-element.selected {
            border-color: #0a7cff;
            box-shadow: 0 0 0 3px rgba(10, 124, 255, 0.15);
        }

        .canvas-element .delete-btn {
            position: absolute;
            top: -10px;
            right: -10px;
            width: 24px;
            height: 24px;
            background: #f44336;
            color: #fff;
            border: none;
            border-radius: 50%;
            font-size: 14px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            line-height: 1;
            box-shadow: 0 2px 8px rgba(244, 67, 54, 0.3);
        }

        .canvas-element.selected .delete-btn {
            display: flex;
        }

        .canvas-element .drag-handle {
            position: absolute;
            top: -6px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 12px;
            color: #b0b8c0;
            cursor: grab;
            display: none;
            background: #fff;
            padding: 0 8px;
            border-radius: 10px;
            border: 1px solid #d0d7de;
        }

        .canvas-element.selected .drag-handle {
            display: block;
        }

        /* ===== ПАНЕЛЬ СВОЙСТВ ===== */
        .properties-panel {
            width: 280px;
            background: #fff;
            border-left: 1px solid #d0d7de;
            padding: 16px 14px;
            overflow-y: auto;
            flex-shrink: 0;
        }

        .properties-panel h4 {
            font-size: 13px;
            color: #6c7a8a;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 12px;
        }

        .prop-group {
            margin-bottom: 14px;
        }

        .prop-group label {
            display: block;
            font-size: 13px;
            font-weight: 500;
            color: #1a1a1a;
            margin-bottom: 4px;
        }

        .prop-group input[type="text"],
        .prop-group input[type="color"],
        .prop-group input[type="number"],
        .prop-group select,
        .prop-group textarea {
            width: 100%;
            padding: 6px 10px;
            border: 1px solid #d0d7de;
            border-radius: 6px;
            font-size: 14px;
            background: #fafbfc;
        }

        .prop-group textarea {
            min-height: 60px;
            resize: vertical;
        }

        .prop-group input[type="color"] {
            height: 40px;
            padding: 2px;
            cursor: pointer;
        }

        .prop-group input:focus,
        .prop-group select:focus,
        .prop-group textarea:focus {
            border-color: #0a7cff;
            outline: none;
            box-shadow: 0 0 0 3px rgba(10, 124, 255, 0.1);
        }

        .prop-group .row {
            display: flex;
            gap: 8px;
        }

        .prop-group .row > * {
            flex: 1;
        }

        .prop-group .btn {
            background: #f1f4f8;
            border: 1px solid #d0d7de;
            border-radius: 6px;
            padding: 6px 12px;
            cursor: pointer;
            font-size: 13px;
        }

        .prop-group .btn.primary {
            background: #0a7cff;
            border-color: #0a7cff;
            color: #fff;
            width: 100%;
        }

        .prop-group .btn.primary:hover {
            background: #0066e0;
        }

        .empty-state {
            color: #9aa8b9;
            font-size: 14px;
            text-align: center;
            padding: 30px 0;
        }

        /* ===== МЕНЮ ВЫБОРА ЭЛЕМЕНТОВ ===== */
        .elements-menu {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #fff;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            padding: 30px;
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            z-index: 100;
            animation: modalIn 0.25s ease;
        }

        .elements-menu.active {
            display: block;
        }

        @keyframes modalIn {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.95); }
            100% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        }

        .elements-menu .menu-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .elements-menu .menu-header h2 {
            font-size: 22px;
            color: #1a1a1a;
        }

        .elements-menu .menu-header .close-btn {
            background: none;
            border: none;
            font-size: 28px;
            color: #9aa8b9;
            cursor: pointer;
            padding: 0 8px;
        }

        .elements-menu .menu-header .close-btn:hover {
            color: #1a1a1a;
        }

        .elements-menu .menu-section {
            margin-bottom: 16px;
        }

        .elements-menu .menu-section h4 {
            font-size: 13px;
            color: #6c7a8a;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 8px;
        }

        .elements-menu .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
            gap: 8px;
        }

        .elements-menu .menu-item {
            background: #f6f9fc;
            border: 1px solid #e4e9f0;
            border-radius: 10px;
            padding: 10px 12px;
            cursor: pointer;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: 0.15s;
            user-select: none;
        }

        .elements-menu .menu-item:hover {
            background: #eef2f7;
            border-color: #c8d0d8;
            transform: translateY(-1px);
        }

        .elements-menu .menu-item .icon {
            font-size: 20px;
            width: 28px;
            text-align: center;
        }

        .elements-menu .menu-item .label {
            font-weight: 500;
        }

        .menu-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.3);
            z-index: 99;
        }

        .menu-overlay.active {
            display: block;
        }

        /* ===== МОДАЛЬНОЕ ОКНО ПУБЛИКАЦИИ ===== */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 200;
            align-items: center;
            justify-content: center;
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal {
            background: #fff;
            border-radius: 20px;
            padding: 40px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: modalIn 0.3s ease;
        }

        .modal h2 {
            font-size: 24px;
            margin-bottom: 8px;
            color: #1a1a1a;
        }

        .modal p {
            color: #6c7a8a;
            margin-bottom: 20px;
            font-size: 14px;
            line-height: 1.6;
        }

        .modal .field {
            margin-bottom: 16px;
        }

        .modal .field label {
            display: block;
            font-weight: 500;
            font-size: 14px;
            margin-bottom: 4px;
            color: #1a1a1a;
        }

        .modal .field input {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid #d0d7de;
            border-radius: 10px;
            font-size: 15px;
            transition: 0.2s;
        }

        .modal .field input:focus {
            border-color: #0a7cff;
            outline: none;
            box-shadow: 0 0 0 3px rgba(10, 124, 255, 0.1);
        }

        .modal .field .hint {
            font-size: 12px;
            color: #9aa8b9;
            margin-top: 4px;
        }

        .modal .actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .modal .actions .btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 10px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
            text-align: center;
        }

        .modal .actions .btn.cancel {
            background: #f1f4f8;
            color: #1a1a1a;
        }

        .modal .actions .btn.cancel:hover {
            background: #e4e9f0;
        }

        .modal .actions .btn.confirm {
            background: #0a7cff;
            color: #fff;
        }

        .modal .actions .btn.confirm:hover {
            background: #0066e0;
        }

        .modal .success-message {
            display: none;
            text-align: center;
            padding: 20px 0;
        }

        .modal .success-message .big-icon {
            font-size: 60px;
            margin-bottom: 12px;
        }

        .modal .success-message h3 {
            font-size: 22px;
            color: #2b9c4c;
            margin-bottom: 6px;
        }

        .modal .success-message .url {
            background: #f1f4f8;
            padding: 10px;
            border-radius: 8px;
            font-size: 16px;
            color: #0a7cff;
            word-break: break-all;
            margin: 12px 0;
        }

        /* ===== СТАТУС ПУБЛИКАЦИИ ===== */
        .publish-status {
            display: none;
            background: #e8f5e9;
            border: 1px solid #a5d6a7;
            border-radius: 8px;
            padding: 8px 16px;
            font-size: 13px;
            color: #2e7d32;
            gap: 8px;
            align-items: center;
        }

        .publish-status.active {
            display: flex;
        }

        .publish-status .url-link {
            color: #0a7cff;
            text-decoration: none;
            font-weight: 500;
        }

        .publish-status .url-link:hover {
            text-decoration: underline;
        }

        /* ===== МОДАЛЬНОЕ ОКНО ЭКСПОРТА HTML ===== */
        .export-modal .modal {
            max-width: 700px;
        }

        .export-modal .code-block {
            background: #1e1e1e;
            color: #d4d4d4;
            padding: 16px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            font-size: 13px;
            max-height: 400px;
            overflow: auto;
            white-space: pre-wrap;
            word-break: break-all;
            margin: 12px 0;
            position: relative;
        }

        .export-modal .code-block .copy-btn {
            position: sticky;
            top: 0;
            float: right;
            background: #0a7cff;
            color: #fff;
            border: none;
            padding: 4px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
        }

        .export-modal .code-block .copy-btn:hover {
            background: #0066e0;
        }

        /* ===== АДАПТИВ ===== */
        @media (max-width: 768px) {
            .properties-panel { width: 100%; max-height: 280px; border-left: none; border-top: 1px solid #d0d7de; }
            .main-area { flex-direction: column; }
            .canvas-wrapper { padding: 10px; }
            .elements-menu .menu-grid { grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); }
            .toolbar .brand small { display: none; }
            .export-modal .modal { padding: 20px; }
        }

        ::-webkit-scrollbar { width: 5px; height: 5px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #c8d0d8; border-radius: 10px; }
    </style>
</head>
<body>

<!-- ===== ВЕРХНЯЯ ПАНЕЛЬ ===== -->
<div class="toolbar">
    <div class="brand">
        🚀 SiteBuilder Pro
        <small>конструктор</small>
    </div>

    <div class="separator"></div>

    <div class="toolbar-group">
        <button class="btn add-element" id="addElementBtn">➕ Добавить блок</button>
    </div>

    <div class="separator"></div>

    <div class="toolbar-group">
        <button class="btn" id="undoBtn">↩ Отменить</button>
        <button class="btn" id="redoBtn">↪ Повторить</button>
    </div>

    <div class="separator"></div>

    <div class="toolbar-group">
        <button class="btn" id="clearBtn">🗑 Очистить</button>
        <button class="btn purple" id="exportCodeBtn">📄 Получить HTML</button>
    </div>

    <div class="separator"></div>

    <div class="toolbar-group">
        <button class="btn" id="previewBtn">👁 Предпросмотр</button>
        <button class="btn success" id="publishBtn">🌐 Опубликовать</button>
    </div>

    <div class="publish-status" id="publishStatus">
        <span>✅ Опубликовано:</span>
        <a href="#" class="url-link" id="statusUrl" target="_blank">site.sitebuilder.com</a>
        <button class="btn" id="statusCopyBtn" style="padding: 2px 10px; font-size: 12px;">📋 Копировать</button>
    </div>
</div>

<!-- ===== ОСНОВНАЯ ОБЛАСТЬ ===== -->
<div class="main-area">
    <div class="canvas-wrapper">
        <div id="siteCanvas">
            <div style="text-align: center; color: #b0b8c0; padding: 40px 0; font-size: 14px;">
                Нажмите «Добавить блок» или перетащите элемент на холст
            </div>
        </div>
    </div>

    <div class="properties-panel" id="propertiesPanel">
        <h4>⚙️ Свойства</h4>
        <div id="propertiesContent">
            <div class="empty-state">
                Выберите элемент на холсте
            </div>
        </div>
    </div>
</div>

<!-- ===== МЕНЮ ВЫБОРА ЭЛЕМЕНТОВ ===== -->
<div class="menu-overlay" id="menuOverlay"></div>
<div class="elements-menu" id="elementsMenu">
    <div class="menu-header">
        <h2>➕ Добавить блок</h2>
        <button class="close-btn" id="closeMenuBtn">×</button>
    </div>

    <div class="menu-section">
        <h4>📦 Базовые</h4>
        <div class="menu-grid">
            <div class="menu-item" data-type="heading"><span class="icon">📝</span><span class="label">Заголовок H1</span></div>
            <div class="menu-item" data-type="subheading"><span class="icon">📌</span><span class="label">Заголовок H2</span></div>
            <div class="menu-item" data-type="text"><span class="icon">📄</span><span class="label">Текст</span></div>
            <div class="menu-item" data-type="button"><span class="icon">🔘</span><span class="label">Кнопка</span></div>
            <div class="menu-item" data-type="image"><span class="icon">🖼</span><span class="label">Изображение</span></div>
            <div class="menu-item" data-type="divider"><span class="icon">➖</span><span class="label">Разделитель</span></div>
        </div>
    </div>

    <div class="menu-section">
        <h4>🎨 Медиа и контент</h4>
        <div class="menu-grid">
            <div class="menu-item" data-type="video"><span class="icon">▶️</span><span class="label">Видео</span></div>
            <div class="menu-item" data-type="card"><span class="icon">🃏</span><span class="label">Карточка</span></div>
            <div class="menu-item" data-type="list"><span class="icon">📋</span><span class="label">Список</span></div>
            <div class="menu-item" data-type="quote"><span class="icon">💬</span><span class="label">Цитата</span></div>
        </div>
    </div>

    <div class="menu-section">
        <h4>🧱 Структура</h4>
        <div class="menu-grid">
            <div class="menu-item" data-type="container"><span class="icon">📦</span><span class="label">Контейнер</span></div>
            <div class="menu-item" data-type="row"><span class="icon">📊</span><span class="label">Колонки (2)</span></div>
            <div class="menu-item" data-type="row3"><span class="icon">📊</span><span class="label">Колонки (3)</span></div>
        </div>
    </div>
</div>

<!-- ===== МОДАЛЬНОЕ ОКНО ПУБЛИКАЦИИ ===== -->
<div class="modal-overlay" id="publishModal">
    <div class="modal">
        <div id="modalForm">
            <h2>🌐 Опубликовать сайт</h2>
            <p>Ваш сайт будет доступен по уникальному адресу в интернете.</p>

            <div class="field">
                <label>Название сайта</label>
                <input type="text" id="siteName" value="Мой сайт">
            </div>

            <div class="field">
                <label>Желаемый адрес (поддомен)</label>
                <input type="text" id="siteSlug" value="mysite">
                <div class="hint">🔗 Ваш сайт: <strong id="previewUrl">mysite.sitebuilder.com</strong></div>
            </div>

            <div class="field">
                <label>Ваш email</label>
                <input type="email" id="siteEmail" placeholder="example@mail.com">
            </div>

            <div class="actions">
                <button class="btn cancel" id="modalCancel">Отмена</button>
                <button class="btn confirm" id="modalPublish">🚀 Опубликовать</button>
            </div>
        </div>

        <div class="success-message" id="modalSuccess">
            <div class="big-icon">🎉</div>
            <h3>Сайт опубликован!</h3>
            <p>Доступен по адресу:</p>
            <div class="url" id="publishedUrl">https://mysite.sitebuilder.com</div>
            <div class="actions" style="margin-top: 16px;">
                <button class="btn confirm" id="modalOpenSite">🔗 Открыть</button>
                <button class="btn cancel" id="modalCloseSuccess">Закрыть</button>
            </div>
        </div>
    </div>
</div>

<!-- ===== МОДАЛЬНОЕ ОКНО ЭКСПОРТА HTML ===== -->
<div class="modal-overlay export-modal" id="exportModal">
    <div class="modal">
        <h2>📄 HTML-код вашего сайта</h2>
        <p>Скопируйте этот код и вставьте в файл с расширением .html — получится полноценный сайт.</p>
        <div class="code-block" id="codeBlock">
            <button class="copy-btn" id="copyCodeBtn">📋 Копировать</button>
            <code id="codeContent">Загрузка...</code>
        </div>
        <div class="actions">
            <button class="btn confirm" id="downloadHtmlBtn">⬇ Скачать .html</button>
            <button class="btn cancel" id="closeExportBtn">Закрыть</button>
        </div>
    </div>
</div>

<script>
    (function() {
        "use strict";

        // ===================== ГЛОБАЛЬНОЕ СОСТОЯНИЕ =====================
        const canvas = document.getElementById('siteCanvas');
        const propsContent = document.getElementById('propertiesContent');

        let elements = [];
        let selectedId = null;
        let nextId = 1;
        let publishedUrl = null;

        // История
        let history = [];
        let historyIndex = -1;
        const MAX_HISTORY = 50;

        // ===================== СОЗДАНИЕ ЭЛЕМЕНТОВ =====================
        function createElementData(type) {
            const base = {
                id: nextId++,
                type: type,
                content: '',
                styles: {}
            };

            switch (type) {
                case 'heading':
                    base.content = 'Заголовок';
                    base.styles = { fontSize: '32px', fontWeight: '700', color: '#1a1a1a', textAlign: 'left', margin: '8px 0' };
                    break;
                case 'subheading':
                    base.content = 'Подзаголовок';
                    base.styles = { fontSize: '24px', fontWeight: '600', color: '#1a1a1a', textAlign: 'left', margin: '6px 0' };
                    break;
                case 'text':
                    base.content = 'Введите ваш текст здесь. Дважды кликните для редактирования.';
                    base.styles = { fontSize: '16px', color: '#333333', lineHeight: '1.7', textAlign: 'left' };
                    break;
                case 'button':
                    base.content = 'Кнопка';
                    base.styles = {
                        display: 'inline-block',
                        padding: '10px 28px',
                        backgroundColor: '#0a7cff',
                        color: '#ffffff',
                        borderRadius: '8px',
                        fontSize: '16px',
                        fontWeight: '600',
                        border: 'none',
                        cursor: 'pointer',
                        textAlign: 'center'
                    };
                    break;
                case 'image':
                    base.content = 'https://via.placeholder.com/600x300/eee/ccc?text=Изображение';
                    base.styles = { maxWidth: '100%', height: 'auto', borderRadius: '8px', display: 'block' };
                    break;
                case 'divider':
                    base.content = '';
                    base.styles = { height: '2px', backgroundColor: '#d0d7de', margin: '16px 0', border: 'none' };
                    break;
                case 'video':
                    base.content = 'https://www.youtube.com/embed/dQw4w9WgXcQ';
                    base.styles = { width: '100%', maxWidth: '560px', height: '315px', borderRadius: '8px', border: 'none' };
                    break;
                case 'card':
                    base.content = 'Карточка';
                    base.styles = {
                        padding: '24px',
                        backgroundColor: '#f6f9fc',
                        borderRadius: '12px',
                        border: '1px solid #e4e9f0',
                        boxShadow: '0 2px 8px rgba(0,0,0,0.04)',
                        margin: '8px 0'
                    };
                    break;
                case 'list':
                    base.content = '• Пункт 1\n• Пункт 2\n• Пункт 3';
                    base.styles = { fontSize: '16px', color: '#333', paddingLeft: '20px', lineHeight: '1.8' };
                    break;
                case 'quote':
                    base.content = '“Ваша цитата здесь. Вдохновляйте своих посетителей.”';
                    base.styles = {
                        fontSize: '20px',
                        fontStyle: 'italic',
                        color: '#444',
                        padding: '16px 24px',
                        borderLeft: '4px solid #0a7cff',
                        backgroundColor: '#f6f9fc',
                        borderRadius: '0 8px 8px 0',
                        margin: '8px 0'
                    };
                    break;
                case 'container':
                    base.content = 'Контейнер';
                    base.styles = {
                        padding: '20px',
                        backgroundColor: '#fafbfc',
                        borderRadius: '12px',
                        border: '1px dashed #c8d0d8',
                        minHeight: '60px',
                        margin: '8px 0'
                    };
                    break;
                case 'row':
                    base.content = 'Колонка 1 | Колонка 2';
                    base.styles = {
                        display: 'grid',
                        gridTemplateColumns: '1fr 1fr',
                        gap: '16px',
                        padding: '12px',
                        backgroundColor: '#f8fafc',
                        borderRadius: '8px',
                        border: '1px dashed #c8d0d8',
                        margin: '8px 0'
                    };
                    break;
                case 'row3':
                    base.content = 'Колонка 1 | Колонка 2 | Колонка 3';
                    base.styles = {
                        display: 'grid',
                        gridTemplateColumns: '1fr 1fr 1fr',
                        gap: '16px',
                        padding: '12px',
                        backgroundColor: '#f8fafc',
                        borderRadius: '8px',
                        border: '1px dashed #c8d0d8',
                        margin: '8px 0'
                    };
                    break;
                default:
                    base.content = 'Элемент';
                    base.styles = { padding: '10px', backgroundColor: '#f0f2f5' };
            }
            return base;
        }

        function addElement(type, insertIndex = -1) {
            const el = createElementData(type);
            if (insertIndex >= 0 && insertIndex < elements.length) {
                elements.splice(insertIndex, 0, el);
            } else {
                elements.push(el);
            }
            selectElement(el.id);
            saveHistory();
            render();
            return el;
        }

        function deleteElement(id) {
            const idx = elements.findIndex(e => e.id === id);
            if (idx === -1) return;
            elements.splice(idx, 1);
            if (selectedId === id) selectedId = null;
            saveHistory();
            render();
            renderProperties();
        }

        function selectElement(id) {
            selectedId = id;
            render();
            renderProperties();
        }

        // ===================== ИСТОРИЯ =====================
        function saveHistory() {
            history = history.slice(0, historyIndex + 1);
            const snapshot = JSON.stringify(elements);
            history.push(snapshot);
            if (history.length > MAX_HISTORY) history.shift();
            historyIndex = history.length - 1;
        }

        function undo() {
            if (historyIndex > 0) { historyIndex--; restoreFromHistory(); }
        }

        function redo() {
            if (historyIndex < history.length - 1) { historyIndex++; restoreFromHistory(); }
        }

        function restoreFromHistory() {
            const snapshot = history[historyIndex];
            if (snapshot) {
                elements = JSON.parse(snapshot);
                const maxId = elements.reduce((max, e) => (e.id > max ? e.id : max), 0);
                nextId = maxId + 1;
                selectedId = null;
                render();
                renderProperties();
            }
        }

        // ===================== ОТРИСОВКА ХОЛСТА =====================
        function render() {
            canvas.innerHTML = '';
            if (elements.length === 0) {
                canvas.innerHTML = `<div style="text-align: center; color: #b0b8c0; padding: 40px 0; font-size: 14px;">Нажмите «Добавить блок» или перетащите элемент на холст</div>`;
                return;
            }

            for (const el of elements) {
                const div = document.createElement('div');
                div.className = 'canvas-element';
                if (selectedId === el.id) div.classList.add('selected');
                div.dataset.id = el.id;

                for (const [key, value] of Object.entries(el.styles)) {
                    div.style[key] = value;
                }

                // Содержимое
                if (el.type === 'image') {
                    const img = document.createElement('img');
                    img.src = el.content || 'https://via.placeholder.com/600x300/eee/ccc?text=Изображение';
                    img.alt = 'Изображение';
                    img.style.width = '100%';
                    img.style.maxWidth = '100%';
                    img.style.borderRadius = '8px';
                    div.appendChild(img);
                } else if (el.type === 'video') {
                    const iframe = document.createElement('iframe');
                    iframe.src = el.content;
                    iframe.style.width = '100%';
                    iframe.style.maxWidth = '560px';
                    iframe.style.height = '315px';
                    iframe.style.border = 'none';
                    iframe.style.borderRadius = '8px';
                    iframe.allow = 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture';
                    iframe.allowFullscreen = true;
                    div.appendChild(iframe);
                } else if (el.type === 'divider') {
                    // уже стилизован
                } else if (el.type === 'list') {
                    const lines = el.content.split('\n').filter(l => l.trim());
                    const ul = document.createElement('ul');
                    ul.style.margin = '0';
                    ul.style.paddingLeft = '20px';
                    for (const line of lines) {
                        const li = document.createElement('li');
                        li.textContent = line.replace(/^[•\-]\s*/, '');
                        ul.appendChild(li);
                    }
                    div.appendChild(ul);
                } else {
                    if (el.type === 'row' || el.type === 'row3') {
                        const parts = el.content.split('|').map(s => s.trim());
                        const wrapper = document.createElement('div');
                        wrapper.style.display = 'contents';
                        for (const part of parts) {
                            const cell = document.createElement('div');
                            cell.textContent = part || 'Колонка';
                            cell.style.padding = '8px';
                            cell.style.backgroundColor = '#fff';
                            cell.style.borderRadius = '6px';
                            cell.style.border = '1px solid #e4e9f0';
                            wrapper.appendChild(cell);
                        }
                        div.appendChild(wrapper);
                    } else {
                        div.textContent = el.content || ' ';
                    }
                }

                // Кнопка удаления
                const delBtn = document.createElement('button');
                delBtn.className = 'delete-btn';
                delBtn.textContent = '×';
                delBtn.addEventListener('mousedown', (e) => {
                    e.stopPropagation();
                    deleteElement(el.id);
                });
                div.appendChild(delBtn);

                // Drag handle
                const handle = document.createElement('div');
                handle.className = 'drag-handle';
                handle.textContent = '↕';
                div.appendChild(handle);

                // Клик для выбора
                div.addEventListener('click', (e) => {
                    if (e.target === delBtn) return;
                    selectElement(el.id);
                });

                // Двойной клик для редактирования текста
                div.addEventListener('dblclick', (e) => {
                    if (['image', 'video', 'divider'].includes(el.type)) return;
                    const currentText = el.content;
                    const input = document.createElement('input');
                    input.type = 'text';
                    input.value = currentText;
                    input.style.cssText = `
                        width: 100%;
                        padding: 4px 8px;
                        border: 2px solid #0a7cff;
                        border-radius: 6px;
                        font-size: inherit;
                        font-family: inherit;
                        background: #fff;
                    `;
                    div.textContent = '';
                    div.appendChild(input);
                    input.focus();
                    input.select();

                    const finish = () => {
                        const newText = input.value.trim() || ' ';
                        el.content = newText;
                        saveHistory();
                        render();
                        renderProperties();
                    };

                    input.addEventListener('blur', finish);
                    input.addEventListener('keydown', (ev) => {
                        if (ev.key === 'Enter') { ev.preventDefault(); input.blur(); }
                        if (ev.key === 'Escape') { input.value = currentText; input.blur(); }
                    });
                });

                canvas.appendChild(div);
            }
        }

        // ===================== ПАНЕЛЬ СВОЙСТВ =====================
        function renderProperties() {
            if (!selectedId) {
                propsContent.innerHTML = `<div class="empty-state">Выберите элемент на холсте</div>`;
                return;
            }
            const el = elements.find(e => e.id === selectedId);
            if (!el) {
                propsContent.innerHTML = `<div class="empty-state">Элемент не найден</div>`;
                return;
            }

            let html = `
                <div class="prop-group">
                    <label>Тип</label>
                    <input type="text" value="${el.type}" disabled style="background:#f1f4f8;">
                </div>
                <div class="prop-group">
                    <label>Содержимое</label>
                    <textarea id="propContent" rows="2">${escapeHtml(el.content)}</textarea>
                </div>
                <div class="prop-group">
                    <label>Цвет текста</label>
                    <input type="color" id="propColor" value="${el.styles.color || '#000000'}">
                </div>
                <div class="prop-group">
                    <label>Размер шрифта</label>
                    <input type="text" id="propFontSize" value="${el.styles.fontSize || '16px'}" placeholder="16px">
                </div>
                <div class="prop-group">
                    <label>Фон</label>
                    <input type="color" id="propBg" value="${el.styles.backgroundColor || '#ffffff'}">
                </div>
                <div class="prop-group">
                    <label>Выравнивание</label>
                    <select id="propAlign">
                        <option value="left" ${el.styles.textAlign === 'left' ? 'selected' : ''}>По левому краю</option>
                        <option value="center" ${el.styles.textAlign === 'center' ? 'selected' : ''}>По центру</option>
                        <option value="right" ${el.styles.textAlign === 'right' ? 'selected' : ''}>По правому краю</option>
                    </select>
                </div>
                <div class="prop-group">
                    <button class="btn primary" id="applyPropsBtn">Применить</button>
                </div>
            `;

            propsContent.innerHTML = html;

            document.getElementById('applyPropsBtn')?.addEventListener('click', () => {
                const content = document.getElementById('propContent')?.value || '';
                const color = document.getElementById('propColor')?.value || '#000000';
                const fontSize = document.getElementById('propFontSize')?.value || '16px';
                const bg = document.getElementById('propBg')?.value || '#ffffff';
                const align = document.getElementById('propAlign')?.value || 'left';

                const el2 = elements.find(e => e.id === selectedId);
                if (!el2) return;

                el2.content = content;
                el2.styles.color = color;
                el2.styles.fontSize = fontSize;
                el2.styles.backgroundColor = bg;
                el2.styles.textAlign = align;

                if (el2.type === 'button') {
                    el2.styles.backgroundColor = bg;
                    el2.styles.color = color;
                }

                saveHistory();
                render();
                renderProperties();
            });
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // ===================== ГЕНЕРАЦИЯ HTML-КОДА САЙТА =====================
        function generateSiteHTML() {
            let html = `<!DOCTYPE html>
        <html lang="ru">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Мой сайт</title>
            <style>
                * { margin: 0; padding: 0; box-sizing: border-box; font-family: system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif; }
                body { padding: 20px; background: #f5f7fa; }
                .page { max-width: 1000px; margin: 0 auto; background: #fff; padding: 30px; border-radius: 16px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); }
        `;

            for (const el of elements) {
                const selector = `.el-${el.id}`;
                html += `${selector} { `;
                for (const [key, value] of Object.entries(el.styles)) {
                    html += `${key}: ${value}; `;
                }
                html += ` }\n`;
            }

            html += `</style></head><body><div class="page">\n`;

            for (const el of elements) {
                const cls = `el-${el.id}`;
                if (el.type === 'image') {
                    html += `<div class="${cls}"><img src="${el.content || 'https://via.placeholder.com/600x300/eee/ccc?text=Изображение'}" alt="image" style="max-width:100%;"></div>\n`;
                } else if (el.type === 'video') {
                    html += `<div class="${cls}"><iframe src="${el.content}" style="width:100%;max-width:560px;height:315px;border:none;border-radius:8px;" allowfullscreen></iframe></div>\n`;
                } else if (el.type === 'divider') {
                    html += `<div class="${cls}"></div>\n`;
                } else if (el.type === 'list') {
                    const lines = el.content.split('\n').filter(l => l.trim());
                    html += `<div class="${cls}"><ul style="margin:0;padding-left:20px;">`;
                    for (const line of lines) {
                        html += `<li>${line.replace(/^[•\-]\s*/, '')}</li>`;
                    }
                    html += `</ul></div>\n`;
                } else if (el.type === 'row' || el.type === 'row3') {
                    const parts = el.content.split('|').map(s => s.trim());
                    const cols = el.type === 'row3' ? 3 : 2;
                    html += `<div class="${cls}" style="display:grid;grid-template-columns:repeat(${cols},1fr);gap:16px;">`;
                    for (const part of parts) {
                        html += `<div style="padding:12px;background:#f8fafc;border-radius:8px;border:1px solid #e4e9f0;">${part || 'Колонка'}</div>`;
                    }
                    html += `</div>\n`;
                } else {
                    html += `<div class="${cls}">${el.content}</div>\n`;
                }
            }

            html += `</div></body></html>`;
            return html;
        }

        // ===================== ЭКСПОРТ HTML (МОДАЛКА) =====================
        function showExportModal() {
            const modal = document.getElementById('exportModal');
            const codeContent = document.getElementById('codeContent');
            const htmlCode = generateSiteHTML();
            codeContent.textContent = htmlCode;
            modal.classList.add('active');
        }

        function closeExportModal() {
            document.getElementById('exportModal').classList.remove('active');
        }

        function copyCode() {
            const code = document.getElementById('codeContent').textContent;
            navigator.clipboard.writeText(code).then(() => {
                const btn = document.getElementById('copyCodeBtn');
                btn.textContent = '✅ Скопировано!';
                setTimeout(() => { btn.textContent = '📋 Копировать'; }, 2000);
            }).catch(() => {
                // Fallback
                const range = document.createRange();
                const codeEl = document.getElementById('codeContent');
                range.selectNode(codeEl);
                window.getSelection().removeAllRanges();
                window.getSelection().addRange(range);
                document.execCommand('copy');
                const btn = document.getElementById('copyCodeBtn');
                btn.textContent = '✅ Скопировано!';
                setTimeout(() => { btn.textContent = '📋 Копировать'; }, 2000);
            });
        }

        function downloadHTML() {
            const html = generateSiteHTML();
            const blob = new Blob([html], { type: 'text/html;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'mysite.html';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // ===================== ПУБЛИКАЦИЯ =====================
        function publishSite() {
            const modal = document.getElementById('publishModal');
            const form = document.getElementById('modalForm');
            const success = document.getElementById('modalSuccess');
            const slug = document.getElementById('siteSlug').value || 'mysite';
            const url = `https://${slug}.sitebuilder.com`;

            const publishedData = {
                name: document.getElementById('siteName').value || 'Мой сайт',
                slug: slug,
                email: document.getElementById('siteEmail').value || 'user@example.com',
                url: url,
                elements: elements,
                publishedAt: new Date().toISOString()
            };
            localStorage.setItem('published_site', JSON.stringify(publishedData));
            publishedUrl = url;

            const statusEl = document.getElementById('publishStatus');
            statusEl.classList.add('active');
            document.getElementById('statusUrl').textContent = url;
            document.getElementById('statusUrl').href = url;

            form.style.display = 'none';
            success.style.display = 'block';
            document.getElementById('publishedUrl').textContent = url;

            document.getElementById('modalOpenSite').onclick = () => {
                window.open(url, '_blank');
            };

            document.getElementById('modalCloseSuccess').onclick = () => {
                modal.classList.remove('active');
                form.style.display = 'block';
                success.style.display = 'none';
            };

            document.getElementById('statusCopyBtn').onclick = () => {
                navigator.clipboard.writeText(url).then(() => {
                    const btn = document.getElementById('statusCopyBtn');
                    btn.textContent = '✅ Скопировано!';
                    setTimeout(() => { btn.textContent = '📋 Копировать'; }, 2000);
                }).catch(() => {
                    alert('Скопируйте адрес вручную: ' + url);
                });
            };
        }

        // ===================== ОЧИСТКА =====================
        function clearCanvas() {
            if (elements.length === 0) return;
            if (!confirm('Удалить все элементы?')) return;
            elements = [];
            selectedId = null;
            nextId = 1;
            saveHistory();
            render();
            renderProperties();
        }

        // ===================== ПРЕДПРОСМОТР =====================
        function preview() {
            const win = window.open('', '_blank');
            if (!win) {
                alert('Разрешите всплывающие окна для предпросмотра');
                return;
            }
            const html = generateSiteHTML();
            win.document.write(html);
            win.document.close();
        }

        // ===================== DRAG & DROP =====================
        function initDragDrop() {
            canvas.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'copy';
            });

            canvas.addEventListener('drop', (e) => {
                e.preventDefault();
                const type = e.dataTransfer.getData('type');
                if (!type) return;
                const elementsRects = canvas.querySelectorAll('.canvas-element');
                let insertIndex = elements.length;
                for (let i = 0; i < elementsRects.length; i++) {
                    const r = elementsRects[i].getBoundingClientRect();
                    const midY = r.top + r.height / 2;
                    if (e.clientY < midY) {
                        insertIndex = i;
                        break;
                    }
                }
                addElement(type, insertIndex);
            });
        }

        // ===================== МЕНЮ ЭЛЕМЕНТОВ =====================
        function openElementsMenu() {
            document.getElementById('elementsMenu').classList.add('active');
            document.getElementById('menuOverlay').classList.add('active');
        }

        function closeElementsMenu() {
            document.getElementById('elementsMenu').classList.remove('active');
            document.getElementById('menuOverlay').classList.remove('active');
        }

        function initElementsMenu() {
            const menuItems = document.querySelectorAll('.menu-item');
            for (const item of menuItems) {
                item.addEventListener('click', () => {
                    const type = item.dataset.type;
                    addElement(type);
                    closeElementsMenu();
                });
            }

            document.getElementById('addElementBtn').addEventListener('click', openElementsMenu);
            document.getElementById('closeMenuBtn').addEventListener('click', closeElementsMenu);
            document.getElementById('menuOverlay').addEventListener('click', closeElementsMenu);
            document.addEventListener('keydown', (e) => {
                if (e.key === 'Escape') closeElementsMenu();
            });
        }

        // ===================== ОБНОВЛЕНИЕ ПРЕДПРОСМОТРА АДРЕСА =====================
        function updatePreviewUrl() {
            const slug = document.getElementById('siteSlug').value || 'mysite';
            document.getElementById('previewUrl').textContent = `${slug}.sitebuilder.com`;
        }

        // ===================== ИНИЦИАЛИЗАЦИЯ =====================
        function init() {
            // Начальные элементы
            const h1 = createElementData('heading');
            h1.content = 'Добро пожаловать в SiteBuilder Pro!';
            elements.push(h1);

            const text = createElementData('text');
            text.content = 'Нажмите «Добавить блок» для вставки новых элементов. Дважды кликните для редактирования.';
            elements.push(text);

            const btn = createElementData('button');
            btn.content = 'Начать';
            elements.push(btn);

            nextId = elements.reduce((max, e) => (e.id > max ? e.id : max), 0) + 1;

            saveHistory();
            render();
            renderProperties();
            initDragDrop();
            initElementsMenu();

            // Кнопки
            document.getElementById('undoBtn').addEventListener('click', undo);
            document.getElementById('redoBtn').addEventListener('click', redo);
            document.getElementById('clearBtn').addEventListener('click', clearCanvas);
            document.getElementById('previewBtn').addEventListener('click', preview);

            // Экспорт HTML
            document.getElementById('exportCodeBtn').addEventListener('click', showExportModal);
            document.getElementById('closeExportBtn').addEventListener('click', closeExportModal);
            document.getElementById('copyCodeBtn').addEventListener('click', copyCode);
            document.getElementById('downloadHtmlBtn').addEventListener('click', downloadHTML);
            document.getElementById('exportModal').addEventListener('click', (e) => {
                if (e.target === e.currentTarget) closeExportModal();
            });

            // Публикация
            document.getElementById('publishBtn').addEventListener('click', () => {
                const modal = document.getElementById('publishModal');
                modal.classList.add('active');
                document.getElementById('modalForm').style.display = 'block';
                document.getElementById('modalSuccess').style.display = 'none';
                updatePreviewUrl();
            });

            document.getElementById('modalCancel').addEventListener('click', () => {
                document.getElementById('publishModal').classList.remove('active');
            });

            document.getElementById('modalPublish').addEventListener('click', publishSite);

            document.getElementById('siteSlug').addEventListener('input', updatePreviewUrl);

            document.getElementById('publishModal').addEventListener('click', (e) => {
                if (e.target === e.currentTarget) {
                    e.currentTarget.classList.remove('active');
                    document.getElementById('modalForm').style.display = 'block';
                    document.getElementById('modalSuccess').style.display = 'none';
                }
            });

            // Проверка опубликованного
            const published = localStorage.getItem('published_site');
            if (published) {
                try {
                    const data = JSON.parse(published);
                    publishedUrl = data.url;
                    const statusEl = document.getElementById('publishStatus');
                    statusEl.classList.add('active');
                    document.getElementById('statusUrl').textContent = data.url;
                    document.getElementById('statusUrl').href = data.url;

                    document.getElementById('statusCopyBtn').onclick = () => {
                        navigator.clipboard.writeText(data.url).then(() => {
                            const btn = document.getElementById('statusCopyBtn');
                            btn.textContent = '✅ Скопировано!';
                            setTimeout(() => { btn.textContent = '📋 Копировать'; }, 2000);
                        }).catch(() => {
                            alert('Скопируйте адрес вручную: ' + data.url);
                        });
                    };
                } catch(e) {}
            }
        }

        init();
    })();
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer Community — сообщество программистов</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: #c0c0c0;
            font-family: 'Courier New', 'Times New Roman', serif;
            font-size: 16px;
            line-height: 1.6;
            color: #000000;
            padding: 30px 20px;
        }
        .container {
            max-width: 820px;
            margin: 0 auto;
            background: #ffffff;
            padding: 40px 50px;
            border: 3px solid #000000;
        }
        h1 {
            font-size: 30px;
            font-weight: bold;
            text-align: center;
            border-bottom: 3px double #000000;
            padding-bottom: 12px;
            margin-bottom: 20px;
            font-family: 'Times New Roman', serif;
            letter-spacing: 2px;
        }
        h2 {
            font-size: 22px;
            font-weight: bold;
            margin-top: 28px;
            margin-bottom: 10px;
            font-family: 'Times New Roman', serif;
            border-bottom: 1px solid #000000;
            padding-bottom: 4px;
        }
        h3 {
            font-size: 18px;
            font-weight: bold;
            margin-top: 20px;
            margin-bottom: 8px;
            font-family: 'Times New Roman', serif;
        }
        p {
            margin-bottom: 14px;
            text-indent: 30px;
        }
        ul, ol {
            margin: 10px 0 14px 40px;
        }
        li {
            margin-bottom: 4px;
        }
        hr {
            border: none;
            border-top: 2px dashed #000000;
            margin: 30px 0;
        }
        .signature {
            text-align: right;
            font-family: 'Courier New', monospace;
            font-size: 15px;
            margin-top: 10px;
        }
        .code-block {
            background: #f0f0f0;
            border-left: 4px solid #000000;
            padding: 12px 18px;
            margin: 12px 0 16px 0;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            white-space: pre-wrap;
            overflow-x: auto;
        }
        .meta {
            text-align: center;
            font-size: 14px;
            color: #444444;
            border-bottom: 1px solid #cccccc;
            padding-bottom: 16px;
            margin-bottom: 20px;
        }
        .meta span {
            background: #000000;
            color: #ffffff;
            padding: 2px 10px;
            font-family: 'Courier New', monospace;
            font-size: 13px;
        }
        .footer {
            margin-top: 30px;
            padding-top: 16px;
            border-top: 2px solid #000000;
            text-align: center;
            font-size: 14px;
            font-family: 'Courier New', monospace;
        }
        .blink {
            animation: blink 1.2s step-end infinite;
        }
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        a {
            color: #0000ff;
            text-decoration: underline;
        }
        a:hover {
            background: #ffff00;
        }
        .member-tag {
            background: #000000;
            color: #00ff00;
            padding: 1px 8px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
        }
        .member-tag-founder {
            background: #000000;
            color: #ffff00;
            padding: 1px 8px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
        }
        .quote {
            padding-left: 30px;
            border-left: 3px solid #666666;
            margin: 12px 0;
            font-style: italic;
        }
        .highlight {
            background: #ffffcc;
            padding: 1px 4px;
        }
        .legal-box {
            background: #f8f8f8;
            border: 2px solid #000000;
            padding: 16px 20px;
            margin: 16px 0;
            font-family: 'Courier New', monospace;
            font-size: 14px;
        }
        .legal-box strong {
            font-size: 15px;
        }
        .warning {
            background: #ffcccc;
            border-left: 6px solid #ff0000;
            padding: 10px 16px;
            margin: 12px 0;
            font-weight: bold;
        }
        .contact-info {
            background: #f0f0f0;
            border: 2px solid #000000;
            padding: 16px 20px;
            margin: 16px 0;
        }
        .contact-info p {
            text-indent: 0;
        }
        .email-highlight {
            background: #000000;
            color: #00ff00;
            padding: 2px 10px;
            font-family: 'Courier New', monospace;
            font-size: 15px;
            font-weight: bold;
        }
        @media (max-width: 600px) {
            body { padding: 10px; }
            .container { padding: 20px; }
            h1 { font-size: 22px; }
            ul, ol { margin-left: 20px; }
        }
    </style>
</head>
<body>

<div class="container">

    <h1>TIMER COMMUNITY</h1>

    <div class="meta">
        <span>СООБЩЕСТВО ПРОГРАММИСТОВ</span> &nbsp;|&nbsp; ОСНОВАНО: 2026 &nbsp;|&nbsp; УЧАСТНИКОВ: 2
    </div>

    <div class="warning">
        ⚠ ВНИМАНИЕ! Данный сайт и все его материалы защищены авторским правом. Любое копирование, изменение или присвоение без разрешения автора запрещено!
    </div>

    <p><strong>Timer Community</strong> — это сообщество программистов, которое создаёт контент каждый день. Мы занимаемся веб-разработкой, изучаем новые технологии, делимся опытом и просто хорошо проводим время за кодом. Нас пока двое, но мы активно растем.</p>

    <hr>

    <h2>Кто мы</h2>

    <p><strong>Я</strong> — основатель сообщества. Моя основная специализация — <span class="highlight">HTML-разработка</span>. Я обожаю создавать сайты, особенно в стиле <span class="highlight">Web 1.0</span>. Мне нравится этот ретро-стиль: простые страницы, текст, таблицы, минимум графики, максимум смысла. Кроме HTML, я иногда занимаюсь <span class="highlight">Python</span> и <span class="highlight">JavaScript</span>. Люблю делать полезные скрипты, автоматизировать рутину и экспериментировать с кодом. Также я провожу время в <span class="highlight">Roblox Studio</span> — создаю игры и модели. Имя аккаунта в целях безопасности не могу сообщить, но если встретите меня там — узнаете по стилю.</p>

    <p><strong>Семён</strong> — мой помощник и первый участник сообщества. Его ник — <span class="highlight">Sema61099</span>. Семён помогает мне с проектами, поддерживает сайт, участвует в обсуждениях и генерирует идеи. Он тоже интересуется веб-разработкой и активно учится новому. Семён — надёжный товарищ, и я рад, что он в команде.</p>

    <div class="quote">
        «Мы — Timer Community. Мы создаём контент каждый день. Нас двое, но каждый из нас — целая команда.»
    </div>

    <hr>

    <h2>Наша деятельность</h2>

    <p>Мы стараемся создавать полезный и интересный контент каждый день. Вот чем мы занимаемся:</p>

    <ul>
        <li><strong>Создание сайтов</strong> — я пишу HTML-страницы в стиле Web 1.0. Это наша основная специализация. Мы делаем информационные сайты, статьи, форумы и многое другое.</li>
        <li><strong>Python-скрипты</strong> — я иногда пишу утилиты на Python для автоматизации задач. Это помогает экономить время и делать рутинную работу быстрее.</li>
        <li><strong>JavaScript-интерактив</strong> — добавляем жизнь нашим страницам с помощью JS. Это могут быть простые анимации, калькуляторы, чаты или игры.</li>
        <li><strong>Roblox Studio</strong> — в свободное время я создаю миры и игры. Это мой творческий отдых. Там я тоже применяю программирование (Lua) и дизайн.</li>
        <li><strong>Генерация идей</strong> — мы с Семёном постоянно придумываем новые проекты. Каждый день рождается что-то новое.</li>
    </ul>

    <div class="code-block">
        // Наш ежедневный код
        function createContent() {
            const projects = ['сайт', 'скрипт', 'идея', 'статья'];
            for (let project of projects) {
                console.log('Создаём ' + project + ' для Timer Community');
            }
            return 'Контент готов!';
        }
        
        // Запускаем каждый день
        setInterval(createContent, 86400000);
    </div>

    <hr>

    <h2>Наш стиль — Web 1.0</h2>

    <p>Мы любим стиль <strong>Web 1.0</strong>. Это эстетика раннего интернета: простые страницы, чёткий текст, минимум стилей, максимальная доступность. Никаких сложных фреймворков — только чистый HTML, базовый CSS и немного JS для интерактива. В этом есть своя красота и душа.</p>

    <p>Мы считаем, что контент важнее дизайна. Поэтому наши страницы выглядят как статьи — много текста, чёткая структура, удобочитаемость. Никаких отвлекающих элементов — только информация и код.</p>

    <hr>

    <h2>Правовая защита и лицензия</h2>

    <div class="legal-box">
        <strong>📜 ЛИЦЕНЗИОННОЕ СОГЛАШЕНИЕ TIMER COMMUNITY</strong><br><br>

        <strong>1. Авторские права</strong><br>
        Все материалы, размещённые на данном сайте и в рамках проекта Timer Community (включая, но не ограничиваясь: HTML-код, CSS-стили, JavaScript-скрипты, текстовый контент, изображения, идеи, концепции), являются интеллектуальной собственностью основателя Timer Community и его участников.<br><br>

        <strong>2. Запрет на копирование и использование</strong><br>
        Запрещается полное или частичное копирование, воспроизведение, распространение, модификация, создание производных работ, публичный показ или любое иное использование материалов Timer Community без письменного разрешения автора.<br><br>

        <strong>3. Защита от присвоения</strong><br>
        Любые попытки выдать материалы Timer Community за свои собственные, использовать их в коммерческих целях или присвоить авторство преследуются по закону. Мы оставляем за собой право обращаться в суд для защиты своих прав.<br><br>

        <strong>4. Лицензия на использование</strong><br>
        Данный сайт и его содержимое предоставляются <strong>«КАК ЕСТЬ»</strong> (AS IS) для ознакомительных целей. Любое использование материалов возможно ТОЛЬКО с явного согласия автора. Для получения разрешения свяжитесь с нами по почте, указанной ниже.<br><br>

        <strong>5. Ответственность</strong><br>
        Автор не несёт ответственности за любой ущерб, возникший в результате использования или невозможности использования материалов сайта.<br><br>

        <strong>6. Действие лицензии</strong><br>
        Данная лицензия действует бессрочно на всей территории Земли и распространяется на все версии и производные работы.<br><br>

        <span style="font-size: 13px; color: #444444;">© 2026 Timer Community. Все права защищены.</span>
    </div>

    <div class="warning">
        ⚡ НАРУШЕНИЕ АВТОРСКИХ ПРАВ ВЛЕЧЕТ ЗА СОБОЙ ОТВЕТСТВЕННОСТЬ СОГЛАСНО ЗАКОНОДАТЕЛЬСТВУ РФ И МЕЖДУНАРОДНЫМ ДОГОВОРАМ.
    </div>

    <p>Мы серьёзно относимся к защите нашего контента. Все материалы создаются с душой и большим трудом. Мы не хотим, чтобы кто-то портил наши работы, присваивал их или использовал без разрешения. Если вы хотите использовать что-то из наших материалов — просто спросите нас. Мы открыты к сотрудничеству и диалогу.</p>

    <p><strong>Как мы защищаем сайт:</strong></p>
    <ul>
        <li><strong>Водяные знаки</strong> — на всех страницах указано авторство Timer Community.</li>
        <li><strong>Мета-теги</strong> — в коде страниц прописаны авторские мета-теги и копирайт.</li>
        <li><strong>Правовые предупреждения</strong> — мы размещаем предупреждения о защите авторских прав.</li>
        <li><strong>Регистрация</strong> — мы планируем зарегистрировать права на наш контент в установленном порядке.</li>
        <li><strong>Мониторинг</strong> — мы отслеживаем использование наших материалов в сети.</li>
    </ul>

    <hr>

    <h2>Контакты</h2>

    <div class="contact-info">
        <p style="text-indent: 0;"><strong>Связаться с нами:</strong></p>
        <p style="text-indent: 0;">✉ <strong>Email:</strong> <span class="email-highlight">timer-com484@gmail.ru</span></p>
        <p style="text-indent: 0;">🐙 <strong>GitHub:</strong> github.com/timer-community (скоро)</p>
        <p style="text-indent: 0; font-size: 14px; color: #444444; margin-top: 6px;">
            * Пишите нам по любым вопросам. Мы открыты к диалогу!
        </p>
    </div>

    <p>Если у вас есть вопросы, предложения или вы хотите использовать наши материалы — напишите нам на <strong>timer-com484@gmail.ru</strong>. Мы всегда отвечаем.</p>

    <hr>

    <h2>Наши планы</h2>

    <p>Timer Community не стоит на месте. Мы планируем:</p>

    <ol>
        <li><strong>Расширяться</strong> — приглашать новых участников. Ищем людей, которые разделяют нашу любовь к Web 1.0, HTML, Python и созданию контента.</li>
        <li><strong>Запустить блог</strong> — будем публиковать статьи о разработке, советы, ретроспективы и идеи.</li>
        <li><strong>Сделать галерею проектов</strong> — покажем, что мы создали. Это будет вдохновлять нас и других.</li>
        <li><strong>Организовать онлайн-встречи</strong> — когда нас станет больше, будем проводить встречи и хакатоны.</li>
        <li><strong>Создать open-source-проекты</strong> — выкладывать наши наработки в открытый доступ (но только те, которые мы решим открыть).</li>
    </ol>

    <hr>

    <h2>Как вступить</h2>

    <p>Если вы программист или просто увлечённый человек, который любит создавать контент — напишите нам на <strong>timer-com484@gmail.ru</strong>. Мы пока небольшие, но нас это не останавливает. Главное — желание работать и интерес к тому, что мы делаем.</p>

    <p><strong>Текущий состав:</strong></p>
    <ul>
        <li><span class="member-tag-founder">[FOUNDER]</span> Я — HTML, Python, JS, Roblox Studio</li>
        <li><span class="member-tag">[MEMBER]</span> Sema61099 (Семён) — помощник, идеи, поддержка</li>
    </ul>

    <p><em>P.S. Мы открыты для общения. Если вам близок Web 1.0 — вы наш человек.</em></p>

    <hr>

    <h2>Заключение</h2>

    <p>Timer Community — это мы. Я и Семён (Sema61099). Мы создаём сайты, пишем код, генерируем идеи и делаем это каждый день. Наш стиль — Web 1.0, наша страсть — программирование, наша цель — расти и развиваться.</p>

    <p>Мы защищаем наш контент, потому что он создан с душой. Мы уважаем чужой труд и просим уважать наш. Если вы чувствуете, что вам с нами по пути — пишите на <strong>timer-com484@gmail.ru</strong>. Мы открыты к диалогу, сотрудничеству и новым участникам.</p>

    <div class="signature">
        С уважением,<br>
        основатель Timer Community<br>
        <span style="font-size: 14px; color: #444444;">P.S. Roblox Studio ждёт, но код — прежде всего!</span>
    </div>

    <hr>

    <div class="footer">
        <span class="blink">▌</span> TIMER COMMUNITY — HTML, PYTHON, JS, WEB 1.0, ROBLOX STUDIO <span class="blink">▌</span><br>
        <span style="font-size: 13px; color: #444444;">
            СОЗДАЁМ КОНТЕНТ КАЖДЫЙ ДЕНЬ • 2026 • ПОКА НАС 2, НО БУДЕТ БОЛЬШЕ
        </span><br>
        <span style="font-size: 13px; color: #000000; font-weight: bold;">
            © 2026 TIMER COMMUNITY. ALL RIGHTS RESERVED. ВСЕ ПРАВА ЗАЩИЩЕНЫ.
        </span><br>
        <span style="font-size: 12px; color: #444444;">
            Любое копирование, модификация или использование материалов без разрешения автора запрещено и преследуется по закону.
        </span><br>
        <span style="font-size: 12px; color: #444444;">
            ✉ timer-com484@gmail.ru
        </span>
    </div>

</div>

</body>
</html>

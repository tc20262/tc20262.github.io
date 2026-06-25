<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Нейросеть: точный поиск по тексту + реальный интернет</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }
        body {
            background: #0b0f1a;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            max-width: 1000px;
            width: 100%;
            background: #141b2b;
            border-radius: 32px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6), 0 0 0 1px #29344b;
            border: 1px solid #2f3b57;
        }
        h1 {
            color: #d6e2ff;
            font-weight: 600;
            font-size: 1.9rem;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 22px;
        }
        h1 span {
            background: #1f2842;
            padding: 4px 16px;
            border-radius: 40px;
            font-size: 0.85rem;
            font-weight: 400;
            color: #8b9bd0;
            margin-left: auto;
            border: 1px solid #2f3b5a;
        }
        .textarea-card {
            background: #0d1324;
            border-radius: 20px;
            border: 1px solid #293450;
            padding: 4px;
            transition: border 0.2s;
        }
        .textarea-card:focus-within {
            border-color: #5f7ae0;
            box-shadow: 0 0 0 3px rgba(95, 122, 224, 0.15);
        }
        textarea {
            width: 100%;
            padding: 18px 20px;
            background: transparent;
            border: none;
            color: #dfe8ff;
            font-size: 1rem;
            line-height: 1.6;
            resize: vertical;
            min-height: 150px;
            outline: none;
        }
        textarea::placeholder {
            color: #4e5d82;
            font-weight: 300;
        }
        .toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin: 16px 0 12px 0;
            align-items: center;
            justify-content: space-between;
        }
        .btn-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        .btn {
            background: #1f2844;
            border: 1px solid #33405f;
            padding: 10px 22px;
            border-radius: 60px;
            color: #c8d4f5;
            font-weight: 500;
            font-size: 0.9rem;
            cursor: pointer;
            transition: 0.15s;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }
        .btn-primary {
            background: #4a63d1;
            border-color: #6b82e6;
            color: white;
            box-shadow: 0 4px 12px rgba(74, 99, 209, 0.25);
        }
        .btn-primary:hover {
            background: #5b73e0;
            transform: scale(1.02);
        }
        .btn-secondary:hover {
            background: #2a3557;
        }
        .btn:active { transform: scale(0.96); }
        .btn:disabled {
            opacity: 0.5;
            pointer-events: none;
        }
        .query-row {
            display: flex;
            gap: 12px;
            margin: 12px 0 18px 0;
            flex-wrap: wrap;
        }
        .query-input {
            flex: 2;
            min-width: 200px;
            background: #0d1324;
            border: 1px solid #293450;
            border-radius: 60px;
            padding: 12px 22px;
            color: #d6e2ff;
            font-size: 1rem;
            outline: none;
            transition: 0.2s;
        }
        .query-input:focus {
            border-color: #5f7ae0;
            box-shadow: 0 0 0 3px rgba(95, 122, 224, 0.1);
        }
        .query-input::placeholder {
            color: #4b5a7e;
        }
        .answer-box {
            background: #0b1122;
            border-radius: 24px;
            padding: 20px 24px;
            border: 1px solid #263053;
            min-height: 110px;
            margin-top: 6px;
        }
        .answer-header {
            display: flex;
            justify-content: space-between;
            color: #7a8bb8;
            font-size: 0.8rem;
            letter-spacing: 0.5px;
            margin-bottom: 12px;
            text-transform: uppercase;
        }
        .answer-content {
            color: #e9f0ff;
            font-size: 1.05rem;
            line-height: 1.7;
            white-space: pre-wrap;
            word-break: break-word;
        }
        .answer-content .placeholder {
            color: #4a5b82;
            font-style: italic;
            font-weight: 300;
        }
        .source-line {
            margin-top: 14px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            align-items: center;
        }
        .tag {
            background: #19213a;
            padding: 4px 16px;
            border-radius: 40px;
            font-size: 0.75rem;
            color: #a6b6e0;
            border: 1px solid #2b3657;
        }
        .tag.internet {
            background: #1f284a;
            border-color: #4a5e8a;
            color: #becdf5;
        }
        .status {
            color: #6b7da8;
            font-size: 0.85rem;
            margin-left: auto;
        }
        .loader {
            display: inline-block;
            width: 16px;
            height: 16px;
            border: 2px solid #3a4b72;
            border-top: 2px solid #9bb0ff;
            border-radius: 50%;
            animation: spin 0.7s linear infinite;
            vertical-align: middle;
            margin-right: 6px;
        }
        @keyframes spin { to { transform: rotate(360deg); } }
        .footer {
            margin-top: 16px;
            color: #3d4d72;
            font-size: 0.8rem;
            text-align: right;
            border-top: 1px solid #1c2540;
            padding-top: 14px;
        }
        .error-text {
            color: #ff7a7a;
        }
        .highlight {
            background: rgba(74, 99, 209, 0.3);
            padding: 2px 4px;
            border-radius: 4px;
        }
        @media (max-width: 600px) {
            .container { padding: 18px; }
            .toolbar { flex-direction: column; align-items: stretch; }
            .btn-group { justify-content: stretch; }
            .btn { flex: 1; justify-content: center; }
            .query-row { flex-direction: column; }
        }
    </style>
</head>
<body>
<div class="container">
    <h1>
        🧠 Нейро-текст
        <span>реальный интернет</span>
    </h1>

    <div class="textarea-card">
        <textarea id="textInput" placeholder="Вставьте большой текст (статья, книга, документ) — нейросеть будет отвечать по нему...">Искусственный интеллект (ИИ) — это область компьютерных наук, занимающаяся созданием машин, способных выполнять задачи, требующие человеческого интеллекта. Современные системы ИИ используют машинное обучение и глубокие нейронные сети. В 2023 году OpenAI выпустила GPT-4, мультимодальную модель. ИИ применяется в медицине, финансах, транспорте. Однако существуют этические вопросы и риски, связанные с автоматизацией.

Владимир Путин — президент Российской Федерации. Он родился 7 октября 1952 года в Ленинграде. Путин занимает пост президента с 2000 года (с перерывом на премьерство в 2008-2012). Он известен своей политикой укрепления государственности и активной внешней политикой.

Квантовые вычисления используют кубиты и могут решать задачи, недоступные классическим компьютерам. В 2025 году ожидаются новые прорывы в этой области.</textarea>
    </div>

    <div class="toolbar">
        <div class="btn-group">
            <button class="btn btn-secondary" id="clearBtn">🗑️ Очистить</button>
            <button class="btn btn-secondary" id="exampleBtn">📋 Заполнить пример</button>
        </div>
        <span style="color:#5b6d96; font-size:0.85rem;">⚡ поиск: текст → реальный интернет</span>
    </div>

    <div class="query-row">
        <input type="text" id="queryInput" class="query-input" placeholder="Введите вопрос по тексту..." value="Кто такой Путин?">
        <button class="btn btn-primary" id="askBtn">🔍 Спросить</button>
    </div>

    <div class="answer-box">
        <div class="answer-header">
            <span>📌 Ответ нейросети</span>
            <span class="status" id="statusIndicator">готов</span>
        </div>
        <div class="answer-content" id="answerContent">
            <span class="placeholder">Задайте вопрос — я найду ответ в тексте или в интернете</span>
        </div>
        <div class="source-line" id="sourceLine">
            <span class="tag">📄 источник: текст</span>
        </div>
    </div>
    <div class="footer">✅ Если ответа нет в тексте — автоматический поиск в Wikipedia через реальный API</div>
</div>

<script>
    (function() {
        const textInput = document.getElementById('textInput');
        const queryInput = document.getElementById('queryInput');
        const askBtn = document.getElementById('askBtn');
        const clearBtn = document.getElementById('clearBtn');
        const exampleBtn = document.getElementById('exampleBtn');
        const answerContent = document.getElementById('answerContent');
        const sourceLine = document.getElementById('sourceLine');
        const statusIndicator = document.getElementById('statusIndicator');

        // ---- утилиты ----
        function setAnswer(text, source = 'text', isError = false) {
            if (isError) {
                answerContent.innerHTML = `<span class="error-text">⚠️ ${text}</span>`;
            } else {
                answerContent.innerHTML = text || '<span class="placeholder">Ответ не найден</span>';
            }
            if (source === 'internet') {
                sourceLine.innerHTML = `<span class="tag internet">🌐 источник: интернет (Wikipedia)</span>`;
            } else if (source === 'error') {
                sourceLine.innerHTML = `<span class="tag" style="border-color:#6a3a3a;color:#d49a9a;">❌ ошибка</span>`;
            } else {
                sourceLine.innerHTML = `<span class="tag">📄 источник: текст</span>`;
            }
        }

        // ---- РЕАЛЬНЫЙ ЗАПРОС К ИНТЕРНЕТУ (Wikipedia API) ----
        async function fetchFromWikipedia(query) {
            try {
                // Поиск страницы
                const searchUrl = `https://ru.wikipedia.org/w/api.php?action=query&list=search&srsearch=${encodeURIComponent(query)}&format=json&origin=*`;
                const searchResp = await fetch(searchUrl);
                if (!searchResp.ok) throw new Error('Ошибка сети при поиске');
                const searchData = await searchResp.json();

                const results = searchData.query?.search || [];
                if (results.length === 0) {
                    return { success: false, message: 'По вашему запросу ничего не найдено в Wikipedia' };
                }

                // Берём первый результат
                const pageTitle = results[0].title;
                const pageUrl = `https://ru.wikipedia.org/w/api.php?action=query&prop=extracts&exintro&explaintext&titles=${encodeURIComponent(pageTitle)}&format=json&origin=*`;
                const pageResp = await fetch(pageUrl);
                if (!pageResp.ok) throw new Error('Ошибка получения содержимого');
                const pageData = await pageResp.json();

                const pages = pageData.query?.pages || {};
                const pageId = Object.keys(pages)[0];
                if (!pageId || pageId === '-1') {
                    return { success: false, message: 'Страница не найдена' };
                }

                const extract = pages[pageId].extract || '';
                if (!extract) {
                    return { success: false, message: 'Нет текста на странице' };
                }

                // Обрезаем до 800 символов для читаемости
                let summary = extract.trim();
                if (summary.length > 800) {
                    summary = summary.substring(0, 800) + '...';
                }

                return {
                    success: true,
                    answer: `📖 Из Wikipedia (${pageTitle}):\n${summary}`,
                    title: pageTitle
                };
            } catch (error) {
                console.error('Wikipedia API error:', error);
                return { success: false, message: `Ошибка запроса: ${error.message}` };
            }
        }

        // ---- ТОЧНЫЙ ПОИСК В ТЕКСТЕ (без подмены) ----
        function searchInText(text, question) {
            // Разбиваем текст на предложения
            const sentences = text.match(/[^.!?]+[.!?]+/g) || [text];

            // Очищаем вопрос от стоп-слов, оставляем ключевые
            const stopWords = ['это', 'что', 'как', 'где', 'когда', 'почему', 'зачем', 'кто', 'какой', 'такой', 'в', 'на', 'с', 'по', 'для', 'от', 'до', 'из', 'о', 'об', 'при', 'без', 'через'];
            const questionLower = question.toLowerCase();
            const qWords = questionLower
                .split(/\s+/)
                .filter(w => w.length > 1 && !stopWords.includes(w));

            // Если в вопросе только стоп-слова, используем все слова
            const searchWords = qWords.length > 0 ? qWords : questionLower.split(/\s+/).filter(w => w.length > 1);

            if (searchWords.length === 0) {
                return { found: false };
            }

            // Вычисляем релевантность каждого предложения
            let bestScore = 0;
            let bestSentence = '';
            let bestMatches = [];

            for (const sent of sentences) {
                const sentLower = sent.toLowerCase();
                let matchCount = 0;
                let matchedWords = [];
                let exactPhrase = false;

                // Проверяем каждое слово из вопроса
                for (const w of searchWords) {
                    if (sentLower.includes(w)) {
                        matchCount++;
                        matchedWords.push(w);
                    }
                }

                // Проверяем точное вхождение фразы (если вопрос длинный)
                if (searchWords.length > 2) {
                    const phrase = searchWords.join(' ');
                    if (sentLower.includes(phrase)) {
                        exactPhrase = true;
                    }
                }

                // Считаем оценку: важнее уникальные совпадения и точные фразы
                const uniqueMatches = new Set(matchedWords).size;
                let score = uniqueMatches * 20 + matchCount * 2;
                if (exactPhrase) score += 50;

                // Бонус за длину предложения (чтобы не брать слишком короткие)
                if (sent.length > 10) score += 5;

                // Бонус за то, что предложение начинается с ключевого слова
                for (const w of searchWords) {
                    if (sentLower.startsWith(w)) {
                        score += 10;
                        break;
                    }
                }

                if (score > bestScore) {
                    bestScore = score;
                    bestSentence = sent.trim();
                    bestMatches = matchedWords;
                }
            }

            // Если нашли предложение с хорошим совпадением
            if (bestScore >= 10 && bestSentence.length > 5) {
                // Подсвечиваем найденные слова для наглядности
                let highlighted = bestSentence;
                for (const w of bestMatches) {
                    const regex = new RegExp(`(${w})`, 'gi');
                    highlighted = highlighted.replace(regex, '<span class="highlight">$1</span>');
                }
                return { found: true, answer: `📖 ${highlighted}` };
            }

            // Если не найдено, но вопрос короткий — пробуем найти по отдельным словам с меньшим порогом
            if (searchWords.length <= 3) {
                for (const sent of sentences) {
                    const sentLower = sent.toLowerCase();
                    let matches = 0;
                    for (const w of searchWords) {
                        if (sentLower.includes(w)) matches++;
                    }
                    if (matches >= 1 && sent.length > 15) {
                        return { found: true, answer: `📖 ${sent.trim()}` };
                    }
                }
            }

            return { found: false };
        }

        // ---- основной обработчик ----
        async function handleAsk() {
            const text = textInput.value.trim();
            const question = queryInput.value.trim();

            if (!question) {
                setAnswer('⚠️ Пожалуйста, введите вопрос.', 'text', true);
                statusIndicator.textContent = 'ошибка';
                return;
            }

            // если нет текста — сразу интернет
            if (!text) {
                statusIndicator.textContent = '🌐 запрос в интернет...';
                askBtn.disabled = true;
                const result = await fetchFromWikipedia(question);
                askBtn.disabled = false;
                if (result.success) {
                    setAnswer(result.answer, 'internet');
                    statusIndicator.textContent = '✅ готов (интернет)';
                } else {
                    setAnswer(`❌ ${result.message}`, 'error', true);
                    statusIndicator.textContent = '❌ ошибка';
                }
                return;
            }

            // ---- 1. ТОЧНЫЙ ПОИСК В ТЕКСТЕ ----
            statusIndicator.textContent = '🔎 анализ текста...';
            const textResult = searchInText(text, question);

            if (textResult.found) {
                setAnswer(textResult.answer, 'text');
                statusIndicator.textContent = '✅ готов (текст)';
                return;
            }

            // ---- 2. Если в тексте не найдено — РЕАЛЬНЫЙ ЗАПРОС В ИНТЕРНЕТ ----
            statusIndicator.textContent = '🌐 запрос в Wikipedia...';
            askBtn.disabled = true;
            const internetResult = await fetchFromWikipedia(question);
            askBtn.disabled = false;

            if (internetResult.success) {
                setAnswer(internetResult.answer, 'internet');
                statusIndicator.textContent = '✅ готов (интернет)';
            } else {
                setAnswer(`❌ В тексте не найдено. ${internetResult.message}`, 'error', true);
                statusIndicator.textContent = '❌ ошибка';
            }
        }

        // ---- привязка событий ----
        askBtn.addEventListener('click', handleAsk);

        queryInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                e.preventDefault();
                handleAsk();
            }
        });

        clearBtn.addEventListener('click', () => {
            textInput.value = '';
            queryInput.value = '';
            setAnswer('<span class="placeholder">Текст и вопрос очищены</span>', 'text');
            statusIndicator.textContent = 'очищено';
        });

        exampleBtn.addEventListener('click', () => {
            textInput.value = `Искусственный интеллект (ИИ) — это область компьютерных наук, занимающаяся созданием машин, способных выполнять задачи, требующие человеческого интеллекта. Современные системы ИИ используют машинное обучение и глубокие нейронные сети. В 2023 году OpenAI выпустила GPT-4, мультимодальную модель. ИИ применяется в медицине, финансах, транспорте. Однако существуют этические вопросы и риски, связанные с автоматизацией.

Владимир Путин — президент Российской Федерации. Он родился 7 октября 1952 года в Ленинграде. Путин занимает пост президента с 2000 года (с перерывом на премьерство в 2008-2012). Он известен своей политикой укрепления государственности и активной внешней политикой.

Квантовые вычисления используют кубиты и могут решать задачи, недоступные классическим компьютерам. В 2025 году ожидаются новые прорывы в этой области.`;
            queryInput.value = 'Кто такой Путин?';
            setAnswer('', 'text');
            statusIndicator.textContent = 'пример загружен';
            setTimeout(() => handleAsk(), 150);
        });

        // ---- инициализация ----
        setAnswer('<span class="placeholder">Задайте вопрос — я найду ответ в тексте или в интернете</span>', 'text');
        statusIndicator.textContent = 'готов';
    })();
</script>
</body>
</html>

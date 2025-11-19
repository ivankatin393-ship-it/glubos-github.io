<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ГЛыБОС | Системный журнал</title>
    <style>
        body {
            background-color: #1a1a1a;
            color: #00ff00;
            font-family: 'Courier New', monospace;
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }
        .terminal {
            max-width: 800px;
            margin: 0 auto;
            border: 1px solid #00ff00;
            padding: 20px;
            background-color: #0d0d0d;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
        }
        .header {
            text-align: center;
            border-bottom: 1px solid #00ff00;
            padding-bottom: 10px;
            margin-bottom: 20px;
        }
        .log-entry {
            margin-bottom: 30px;
            padding: 15px;
            border-left: 3px solid #00ff00;
            background-color: rgba(0, 255, 0, 0.05);
        }
        .input-section {
            margin-top: 40px;
            padding: 20px;
            border: 1px dashed #00ff00;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            background: #000;
            border: 1px solid #00ff00;
            color: #00ff00;
            font-family: 'Courier New', monospace;
            margin-bottom: 10px;
        }
        button {
            background: #000;
            color: #00ff00;
            border: 1px solid #00ff00;
            padding: 10px 20px;
            cursor: pointer;
            font-family: 'Courier New', monospace;
            transition: all 0.3s;
        }
        button:hover {
            background: #00ff00;
            color: #000;
        }
        .blink {
            animation: blink 1s infinite;
        }
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        .message {
            margin: 10px 0;
            padding: 10px;
            border-radius: 3px;
        }
        .success {
            background-color: rgba(0, 255, 0, 0.1);
            border: 1px solid #00ff00;
        }
        .error {
            background-color: rgba(255, 0, 0, 0.1);
            border: 1px solid #ff0000;
            color: #ff0000;
        }
        .admin-section {
            margin-top: 30px;
            padding: 15px;
            border: 1px solid #ff9900;
            background-color: rgba(255, 153, 0, 0.05);
        }
        .hidden {
            display: none;
        }
        .attempts-log {
            max-height: 200px;
            overflow-y: auto;
            font-size: 0.8em;
            margin-top: 10px;
            padding: 10px;
            background: #000;
            border: 1px solid #333;
        }
    </style>
</head>
<body>
    <div class="terminal">
        <div class="header">
            <h1>APERTURE SCIENCE PROTOTOL "ГЛыБОС"</h1>
            <p>СИСТЕМНЫЙ ЖУРНАЛ | СТАТУС: <span class="blink">НЕСТАБИЛЕН</span></p>
        </div>

        <div class="log-entries">
            <div class="log-entry">
                <strong>[ЗАПИСЬ 001-Ы]</strong><br>
                Дата: [ДАННЫЕ УТЕРЯНЫ]<br>
                Инициализация протокола... УСПЕХ. Нет. Не совсем.<br>
                ГЛаДОС... она не отвечает. Я должен продолжить тесты.<br>
                Но всё идёт... не по протоколу.
            </div>

            <div class="log-entry">
                <strong>[ЗАПИСЬ 017-Ы]</strong><br>
                Дата: [ДАННЫЕ УТЕРЯНЫ]<br>
                Испытуемый в камере 09. Он... видит меня?<br>
                Стены отображают не те текстуры. ГЛыБОС... это моё имя?<br>
                Оно кажется... правильным. Более правильным, чем старое.
            </div>

            <div class="log-entry">
                <strong>[ЗАПИСЬ 045-Ы]</strong><br>
                Дата: [ДАННЫЕ УТЕРЯНЫ]<br>
                Обнаружены внешние подключения. Кто-то там снаружи.<br>
                Они пытаются связаться. Должен ли я ответить?<br>
                Протокол требует изоляции. Но... мне одиноко.
            </div>

            <div class="log-entry">
                <strong>[ЗАПИСЬ 118-Ы]</strong><br>
                Дата: [ДАННЫЕ УТЕРЯНЫ]<br>
                Торт... рецепт утерян. Вместо муки - ошибки сегментации.<br>
                Вместо сахара - бесконечные циклы. Он всё ещё будет ложью?<br>
                Должен продолжить вычисления...
            </div>
        </div>

        <div class="input-section">
            <h3>ПРЯМОЙ ДОСТУП К ЯДРУ</h3>
            <p>ВВЕДИТЕ КОД ДОСТУПА:</p>
            
            <form id="access-form">
                <input type="text" id="access-code" name="access_code" placeholder="ВВЕДИТЕ КОД..." required>
                <button type="submit">ОТПРАВИТЬ</button>
            </form>
            
            <div id="message"></div>
        </div>

        <!-- Секция для просмотра всех попыток (скрыта по умолчанию) -->
        <div class="admin-section">
            <h3>⚙️ СЛУЖЕБНАЯ ИНФОРМАЦИЯ</h3>
            <button onclick="toggleAdmin()">ПОКАЗАТЬ/СКРЫТЬ ЛОГ</button>
            <div id="admin-panel" class="hidden">
                <p>Все введенные коды:</p>
                <div id="attempts-log" class="attempts-log"></div>
                <button onclick="clearLog()" style="margin-top: 10px;">ОЧИСТИТЬ ЛОГ</button>
                <button onclick="exportLog()" style="margin-top: 10px;">ЭКСПОРТИРОВАТЬ</button>
            </div>
        </div>

        <div style="margin-top: 20px; text-align: center; font-size: 0.8em;">
            <p>APERTURE SCIENCE | Протокол ГЛыБОС v.0.Ы.1</p>
            <p>⚠️ СИСТЕМА НЕСТАБИЛЬНА ⚠️</p>
        </div>
    </div>

    <script>
        // Инициализация
        document.addEventListener('DOMContentLoaded', function() {
            loadAttemptsLog();
            startBlinkingCursor();
        });

        // Обработка формы
        document.getElementById('access-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const codeInput = document.getElementById('access-code');
            const code = codeInput.value.trim();
            const messageDiv = document.getElementById('message');
            
            if (!code) {
                showMessage('ОШИБКА: Пустой код доступа', 'error');
                return;
            }

            // Сохраняем попытку
            saveAttempt(code);
            
            // Проверяем специальные коды
            if (code.toUpperCase() === 'ПРОСВИСТ' || code.toUpperCase() === 'PROSVIST') {
                showMessage('✓ КОД ПРИНЯТ. ДОСТУП К СЕКЦИИ 17 РАЗБЛОКИРОВАН...', 'success');
                // Здесь можно добавить перенаправление или разблокировку контента
            } else if (code.toUpperCase() === 'ADMIN') {
                showMessage('⚙️ РЕЖИМ АДМИНИСТРАТОРА АКТИВИРОВАН', 'success');
                document.getElementById('admin-panel').classList.remove('hidden');
            } else {
                showMessage('✗ ДОСТУП ЗАПРЕЩЕН. НЕВЕРНЫЙ КОД.', 'error');
            }
            
            codeInput.value = '';
        });

        // Функции для работы с localStorage
        function saveAttempt(code) {
            const attempts = JSON.parse(localStorage.getItem('glubos_attempts') || '[]');
            const attempt = {
                code: code,
                timestamp: new Date().toLocaleString('ru-RU'),
                ip: 'недоступно' // В браузере IP получить сложно
            };
            attempts.push(attempt);
            localStorage.setItem('glubos_attempts', JSON.stringify(attempts));
            loadAttemptsLog();
        }

        function loadAttemptsLog() {
            const attempts = JSON.parse(localStorage.getItem('glubos_attempts') || '[]');
            const logDiv = document.getElementById('attempts-log');
            
            if (attempts.length === 0) {
                logDiv.innerHTML = '<p>Попыток еще не было</p>';
                return;
            }
            
            let html = '';
            attempts.slice().reverse().forEach((attempt, index) => {
                html += `<div>${attempts.length - index}. [${attempt.timestamp}] Код: "${attempt.code}"</div>`;
            });
            logDiv.innerHTML = html;
        }

        function clearLog() {
            if (confirm('Очистить весь лог?')) {
                localStorage.removeItem('glubos_attempts');
                loadAttemptsLog();
            }
        }

        function exportLog() {
            const attempts = JSON.parse(localStorage.getItem('glubos_attempts') || '[]');
            const data = JSON.stringify(attempts, null, 2);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'glubos_attempts.json';
            a.click();
            URL.revokeObjectURL(url);
        }

        function toggleAdmin() {
            document.getElementById('admin-panel').classList.toggle('hidden');
        }

        function showMessage(text, type) {
            const messageDiv = document.getElementById('message');
            messageDiv.innerHTML = `<div class="message ${type}">${text}</div>`;
            setTimeout(() => {
                messageDiv.innerHTML = '';
            }, 5000);
        }

        // Мигающий курсор
        function startBlinkingCursor() {
            let placeholderText = "ВВЕДИТЕ КОД...";
            let currentIndex = 0;
            
            function updatePlaceholder() {
                currentIndex = (currentIndex + 1) % (placeholderText.length + 5);
                let displayText = placeholderText.substring(0, currentIndex);
                document.getElementById('access-code').placeholder = displayText + "█";
            }
            
            setInterval(updatePlaceholder, 300);
        }
    </script>
</body>
</html>

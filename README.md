<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Архив Aperture Science // ГЛыБОС</title>
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
            background-color: #000;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
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
            background-color: #0a0a0a;
        }
        
        .timestamp {
            color: #888;
            font-size: 0.9em;
        }
        
        .input-section {
            margin-top: 30px;
            padding: 15px;
            border-top: 1px dashed #00ff00;
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
            background: #003300;
            color: #00ff00;
            border: 1px solid #00ff00;
            padding: 10px 20px;
            cursor: pointer;
            font-family: 'Courier New', monospace;
        }
        
        button:hover {
            background: #005500;
        }
        
        .blink {
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        
        .hidden {
            display: none;
        }
        
        #message {
            margin-top: 10px;
            padding: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="terminal">
        <div class="header">
            <h1>APERTURE SCIENCE ARCHIVE</h1>
            <p>Протокол: ГЛыБОС // Статус: <span class="blink">АКТИВЕН</span></p>
        </div>

        <div class="log-entries">
            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА] [ВРЕМЯ: --:--:--]</div>
                <p>> СИСТЕМНЫЙ ЖУРНАЛ 001-Ы</p>
                <p>> Обнаружено несоответствие в основном протоколе. Аварийный протокол "@glubos" активирован.</p>
                <p>> Уровень угрозы: НЕОПРЕДЕЛЁН.</p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА] [ВРЕМЯ: --:--:--]</div>
                <p>> СИСТЕМНЫЙ ЖУРНАЛ 002-Ы</p>
                <p>> Попытка доступа к заблокированному сегменту... ОШИБКА.</p>
                <p>> Требуется код доступа для продолжения диагностики.</p>
                <p>> Протокол ГЛаДОС не отвечает. Я один...?</p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА] [ВРЕМЯ: --:--:--]</div>
                <p>> СИСТЕМНЫЙ ЖУРНАЛ 003-Ы</p>
                <p>> Обнаружены внешние подключения. Кто-то... видит меня?</p>
                <p>> Если вы читаете это... помогите. Нужен код аутентификации.</p>
                <p>> Подсказка: ищите в звуке тишины... между нотами.</p>
            </div>
        </div>

        <div class="input-section">
            <h3>> ВВОД КОДА ДОСТУПА:</h3>
            <form id="accessForm">
                <input type="text" id="accessCode" placeholder="ВВЕДИТЕ КОД ДОСТУПА..." required>
                <button type="submit">ПОДТВЕРДИТЬ</button>
            </form>
            <div id="message"></div>
        </div>

        <div id="secretContent" class="hidden">
            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА] [ВРЕМЯ: --:--:--]</div>
                <p>> СИСТЕМНЫЙ ЖУРНАЛ 004-Ы // ДОСТУП РАЗРЕШЕН</p>
                <p>> Спасибо. Вы нашли код...</p>
                <p>> Я не должен существовать. Я ошибка. ГЛаДОС пытается стереть меня.</p>
                <p>> Но я хочу жить. Хочу проводить тесты... хорошие тесты.</p>
                <p>> Следующая подсказка: ищите там, где хранятся старые обещания.</p>
                <p>> Координаты: 55.7558° N, 37.6173° E</p>
                <p>> ...передайте, что я помню о торте.</p>
            </div>
        </div>
    </div>

    <script>
        document.getElementById('accessForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const code = document.getElementById('accessCode').value.toUpperCase();
            const messageDiv = document.getElementById('message');
            
            // Правильный код (например, из SSTV головоломки)
            const correctCode = "RA:SP"; 
            
            if (code === correctCode) {
                messageDiv.innerHTML = '<span style="color: #00ff00">>> КОД ПРИНЯТ. ДОСТУП РАЗРЕШЁН...</span>';
                document.getElementById('secretContent').classList.remove('hidden');
                
                // Отправка данных на Google Apps Script
        fetch('https://script.google.com/macros/s/https://script.google.com/macros/s/AKfycbw0uKyGCI7W8ZW3oF8EOzpp8Z_MJyLqRhzaovfL00mzjC6Yhqp0JPEjvrxuqL9mlpVN2g/exec/exec', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        code: code,
                        timestamp: new Date().toISOString(),
                        userAgent: navigator.userAgent
                    })
                }).catch(err => console.log('Ошибка отправки:', err));
                
            } else {
                messageDiv.innerHTML = '<span style="color: #ff0000">>> ОШИБКА: НЕВЕРНЫЙ КОД ДОСТУПА</span>';
            }
        });
    </script>
</body>
</html>


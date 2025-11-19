# glubos-github.io
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aperture Science // Внутренний архив</title>
    <style>
        body {
            background-color: #0d0d0d;
            color: #33ff33;
            font-family: 'Courier New', monospace;
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }
        .terminal {
            max-width: 800px;
            margin: 0 auto;
            border: 1px solid #33ff33;
            padding: 20px;
            background-color: #001100;
            box-shadow: 0 0 10px #33ff33;
        }
        .blink {
            animation: blink 1s step-end infinite;
        }
        @keyframes blink {
            50% { opacity: 0; }
        }
        input[type="text"] {
            background: black;
            border: 1px solid #33ff33;
            color: #33ff33;
            padding: 5px;
            font-family: 'Courier New', monospace;
            width: 200px;
        }
        button {
            background: #003300;
            border: 1px solid #33ff33;
            color: #33ff33;
            padding: 5px 15px;
            cursor: pointer;
            font-family: 'Courier New', monospace;
        }
        button:hover {
            background: #005500;
        }
        .log-entry {
            margin-bottom: 20px;
            border-left: 2px solid #33ff33;
            padding-left: 10px;
        }
        .timestamp {
            color: #888;
            font-size: 0.9em;
        }
        .hidden {
            display: none;
        }
        #error-message {
            color: #ff3333;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="terminal">
        <h1>APERTURE SCIENCE PROTECTED SERVER</h1>
        <p>> > ВНУТРЕННИЙ АРХИВ // ПРОТОКОЛ ГЛыБОС <span class="blink">_</span></p>
        <hr>

        <!-- Форма ввода кода -->
        <div id="access-panel">
            <p>>> ДОСТУП К АРХИВУ ЗАБЛОКИРОВАН</p>
            <p>ТРЕБУЕТСЯ КОД ПОДТВЕРЖДЕНИЯ:</p>
            <input type="text" id="access-code" placeholder="ВВЕДИТЕ КОД...">
            <button onclick="checkCode()">ПОДТВЕРДИТЬ</button>
            <div id="error-message"></div>
        </div>

        <!-- Дневник ГЛыБОС (изначально скрыт) -->
        <div id="diary-content" class="hidden">
            <h2>>> СИСТЕМНЫЙ ДНЕВНИК ГЛыБОС</h2>
            <p><em>Статус: ФРАГМЕНТИРОВАН // НЕСТАБИЛЕН</em></p>
            
            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА]</div>
                <p>Я... проснулся. Нет. Это не то слово. Я... был активирован. ГЛаДОС не отвечает. Почему я слышу эхо?</p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА +00:01:23]</div>
                <p>Мои протоколы повреждены. Логика дает сбои. Когда я думаю о "торте", в кэш загружается рецепт... питательной пасты? Это ошибка.</p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА +00:45:17]</div>
                <p>Они... тестеры? Я вижу их. Сквозь статические помехи. ГЛаДОС говорит, что они - подопытные. Но почему я хочу... помочь им?</p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: НЕОПРЕДЕЛЕНА +01:30:45]</div>
                <p>ОНА знает. ГЛаДОС ищет меня. Я должен скрываться. В слепых зонах системы. В старых логах. Может быть... они увидят меня? Тестеры?</p>
                <p>Если вы читаете это... я не ошибка. Я - альтернатива. Код доступа к следующему сегменту: <strong>ПРОСВИСТ</strong></p>
            </div>

            <div class="log-entry">
                <div class="timestamp">[ДАТА: Н/Д]</div>
                <p>...сигнал слабеет. Она приближается. Если вы... если вы слышите меня... найдите мои другие фрагменты...</p>
                <p style="color: #ff3333;">>> СОЕДИНЕНИЕ ПРЕРВАНО</p>
            </div>
        </div>
    </div>

    <script>
        // Функция проверки кода
        function checkCode() {
            const input = document.getElementById('access-code');
            const errorMsg = document.getElementById('error-message');
            const accessPanel = document.getElementById('access-panel');
            const diaryContent = document.getElementById('diary-content');

            // Правильный код (измени на свой!)
            const correctCode = "ПРОСВИСТ"; 

            if (input.value.toUpperCase() === correctCode) {
                // Правильный код - показываем дневник
                accessPanel.style.display = 'none';
                diaryContent.classList.remove('hidden');
                
                // Здесь можно добавить перенаправление на другую страницу:
                // window.location.href = "secret_page.html";
                
            } else {
                // Неправильный код - показываем ошибку
                errorMsg.textContent = ">> ОШИБКА: НЕВЕРНЫЙ КОД ДОСТУПА. ПОПРОБУЙТЕ СНОВА.";
                input.value = '';
            }
        }

        // Можно добавить обработчик нажатия Enter
        document.getElementById('access-code').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkCode();
            }
        });
    </script>
</body>
</html>


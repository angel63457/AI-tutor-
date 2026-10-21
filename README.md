<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>School AI Tutor</title>
  <style>
    body { font-family: sans-serif; padding: 1rem; }
    #chat { height: 300px; overflow-y: auto; border: 1px solid #ccc; margin-bottom: 1rem; padding: 0.5rem; }
    .msg { margin: 0.25rem 0; }
    .user { color: #007bff; }
    .ai { color: #28a745; }
    input { padding: 0.5rem; width: 70%; }
    button { padding: 0.5rem 1rem; }
  </style>
</head>
<body>
  <h2>ИИ‑репетитор</h2>
  <div id="chat"></div>
  <input type="text" id="userInput" placeholder="Введите вопрос по предмету...">
  <button onclick="send()">Отправить</button>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('userInput');

    const responses = {
      'математика': 'Давай разберём тему. Например, уравнение 2x + 3 = 7 решается так: 2x = 4 → x = 2. Напиши конкретную задачу — помогу пошагово.',
      'физика': 'Физика — про законы природы. Например, F = ma. Расскажи, какая тема тебя интересует: механика, электричество и т. д.',
      'русский': 'В русском языке важно понимать правила и исключения. Например, «жи‑ши» пиши с «и». Какой раздел нужен: орфография, пунктуация?',
      'привет': 'Привет! Я твой ИИ‑репетитор. Расскажи, какой предмет и тему хочешь разобрать — помогу объяснить просто и по шагам.',
      'default': 'Я пока знаю не всё, но постараюсь помочь. Напиши чуть подробнее, что нужно: тему, класс, пример задачи — и я дам объяснение или задачу для тренировки.'
    };

    function send() {
      const text = input.value.trim().toLowerCase();
      if (!text) return;
      addMessage('Ты', text, 'user');
      input.value = '';

      setTimeout(() => {
        let reply = responses.default;
        for (const key in responses) {
          if (text.includes(key)) {
            reply = responses[key];
            break;
          }
        }
        addMessage('ИИ', reply, 'ai');
      }, 800);
    }

    function addMessage(sender, text, cls) {
      const div = document.createElement('div');
      div.className = `msg \${cls}`;
      div.innerHTML = `<b>${sender}:</b> ${text}`;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }
  </script>
</body>
</html>

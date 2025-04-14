<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Треугольный Квест</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #f0f0f0;
      margin: 0;
    }

    .game-container {
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 320px;
    }

    .triangle {
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 100px solid #009688;
      margin: 20px auto;
    }

    button {
      padding: 10px 20px;
      background-color: #009688;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #00796b;
    }

    input {
      padding: 10px;
      width: 80%;
      margin-top: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    #feedback {
      margin-top: 10px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>Треугольный Квест</h1>
    <div id="triangle" class="triangle"></div>
    <div class="task">
      <p>Найдите недостающий угол:</p>
      <p id="task">Угол 1: 40°, Угол 2: 60°, ?</p>
      <input type="number" id="userAnswer" placeholder="Введите угол" />
      <button onclick="checkAnswer()">Проверить</button>
    </div>
    <div id="feedback"></div>
    <button onclick="nextTask()">Следующая задача</button>
  </div>
  <script>
    let currentTask = 0;
    const tasks = [
      { angles: [40, 60], correctAnswer: 80 },
      { angles: [50, 70], correctAnswer: 60 },
      { angles: [30, 90], correctAnswer: 60 },
      { angles: [45, 45], correctAnswer: 90 },
    ];

    function displayTask() {
      const task = tasks[currentTask];
      document.getElementById('task').innerText = `Угол 1: ${task.angles[0]}°, Угол 2: ${task.angles[1]}°, ?`;
      document.getElementById('feedback').innerText = '';
      document.getElementById('userAnswer').value = '';
    }

    function checkAnswer() {
      const userAnswer = parseInt(document.getElementById('userAnswer').value);
      const correctAnswer = tasks[currentTask].correctAnswer;

      if (userAnswer === correctAnswer) {
        document.getElementById('feedback').innerText = 'Правильный ответ!';
      } else {
        document.getElementById('feedback').innerText = `Неправильно. Правильный ответ: ${correctAnswer}°`;
      }
    }

    function nextTask() {
      if (currentTask < tasks.length - 1) {
        currentTask++;
        displayTask();
      } else {
        document.getElementById('feedback').innerText = 'Поздравляем! Вы прошли все задачи!';
        document.getElementById('task').innerText = '';
        document.getElementById('userAnswer').style.display = 'none';
        document.querySelector('button').style.display = 'none';
      }
    }

    window.onload = displayTask;
  </script>
</body>
</html>

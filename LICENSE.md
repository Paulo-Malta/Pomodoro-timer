<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pomodoro Timer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: white;
            color: #333;
            margin: 0;
            padding: 0;
        }

        h1 {
            margin-top: 20px;
        }

        .container {
            margin: 20px auto;
            width: 300px;
            padding: 20px;
            background: white;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }

        img {
            width: 100px;
            height: 100px;
            margin: 20px 0;
        }

        label {
            display: block;
            margin: 10px 0 5px;
            font-weight: bold;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }

        button {
            width: 100%;
            padding: 10px;
            background: #007BFF;
            color: #fff;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        button:hover {
            background: #0056b3;
        }

        .timer {
            font-size: 48px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <h1>Pomodoro Timer</h1>
    <img src="pomodoro.png.jfif" alt="Pomodoro Icon">
    <div class="container">
        <label for="study-time">Tempo de Estudo (minutos):</label>
        <input type="number" id="study-time" placeholder="Ex: 25">

        <label for="break-time">Tempo de Descanso (minutos):</label>
        <input type="number" id="break-time" placeholder="Ex: 5">

        <button onclick="startTimer()">Iniciar Pomodoro</button>

        <div class="timer" id="timer">00:00</div>
    </div>

    <script>
        let studyTime = 0;
        let breakTime = 0;
        let isStudyTime = true;
        let timerInterval;

        function startTimer() {
            studyTime = parseInt(document.getElementById('study-time').value) || 0;
            breakTime = parseInt(document.getElementById('break-time').value) || 0;

            if (studyTime <= 0 || breakTime <= 0) {
                alert('Por favor, insira tempos válidos de estudo e descanso.');
                return;
            }

            isStudyTime = true;
            startCountdown(studyTime * 60);
        }

        function startCountdown(duration) {
            clearInterval(timerInterval);

            let timeRemaining = duration;
            updateTimerDisplay(timeRemaining);

            timerInterval = setInterval(() => {
                timeRemaining--;
                updateTimerDisplay(timeRemaining);

                if (timeRemaining <= 0) {
                    clearInterval(timerInterval);
                    isStudyTime = !isStudyTime;

                    if (isStudyTime) {
                        alert('Hora de estudar!');
                        startCountdown(studyTime * 60);
                    } else {
                        alert('Hora de descansar!');
                        startCountdown(breakTime * 60);
                    }
                }
            }, 1000);
        }

        function updateTimerDisplay(seconds) {
            const minutes = Math.floor(seconds / 60);
            const remainingSeconds = seconds % 60;
            document.getElementById('timer').textContent = 
                `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
        }
    </script>
</body>
</html>

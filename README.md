# Stopwatch

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: orangered;
            color: white;
            text-align: center;
            margin-top: 170px;
        }
        
        #stopwatch {
            font-size: 100px;
            color: black;
            margin-bottom: 20px;
        }
        
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: white;
            border: 2px solid rgb(233, 7, 45);
            margin: 5px;
            cursor: pointer;
        }
        
        #laps {
            margin-top: 20px;
            list-style: none;
            padding: 0;
        }
        
        #laps li {
            font-size: 18px;
            margin: 5px 0;
        }
    </style>
</head>

<body>
    <h1>Stopwatch</h1>
    <div id="stopwatch">00:00:00</div>
    <button id="start">Start</button>
    <button id="pause">Pause</button>
    <button id="reset">Reset</button>
    <button id="lap">Lap</button>

    <ul id="laps"></ul>

    <script>
        let timerInterval;
        let elapsedTime = 0;
        let isRunning = false;

        const stopwatch = document.getElementById('stopwatch');
        const laps = document.getElementById('laps');

        function formatTime(time) {
            const milliseconds = Math.floor((time % 1000) / 10);
            const seconds = Math.floor((time / 1000) % 60);
            const minutes = Math.floor((time / 60000) % 60);
            return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}:${String(milliseconds).padStart(2, '0')}`;
        }

        function updateDisplay() {
            stopwatch.textContent = formatTime(elapsedTime);
        }

        function startTimer() {
            if (!isRunning) {
                const startTime = Date.now() - elapsedTime;
                timerInterval = setInterval(() => {
                    elapsedTime = Date.now() - startTime;
                    updateDisplay();
                }, 10);
                isRunning = true;
            }
        }

        function pauseTimer() {
            clearInterval(timerInterval);
            isRunning = false;
        }

        function resetTimer() {
            clearInterval(timerInterval);
            elapsedTime = 0;
            isRunning = false;
            updateDisplay();
            laps.innerHTML = '';
        }

        function recordLap() {
            if (isRunning) {
                const lapTime = document.createElement('li');
                lapTime.textContent = formatTime(elapsedTime);
                laps.appendChild(lapTime);
            }
        }

        document.getElementById('start').addEventListener('click', startTimer);
        document.getElementById('pause').addEventListener('click', pauseTimer);
        document.getElementById('reset').addEventListener('click', resetTimer);
        document.getElementById('lap').addEventListener('click', recordLap);

        updateDisplay();
    </script>
</body>

</html>

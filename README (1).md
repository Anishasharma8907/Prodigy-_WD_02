<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="stopwatch">
        <h1>Stopwatch</h1>
        <div id="time">00:00:00</div>
        <div class="buttons">
            <button id="start">Start</button>
            <button id="pause">Pause</button>
            <button id="reset">Reset</button>
        </div>
        <ul id="laps"></ul>
    </div>
    <script src="script.js"></script>
</body>
</html>

/* styles.css */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f4f4f9;
    margin: 0;
    padding: 20px;
}

.stopwatch {
    max-width: 300px;
    margin: 50px auto;
    padding: 20px;
    background: #fff;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

#time {
    font-size: 2.5rem;
    margin: 20px 0;
}

.buttons button {
    padding: 10px 20px;
    margin: 5px;
    font-size: 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background-color: #007bff;
    color: white;
}

.buttons button:hover {
    background-color: #0056b3;
}

#laps {
    list-style: none;
    padding: 0;
    margin-top: 20px;
}

#laps li {
    font-size: 1rem;
    padding: 5px;
    background: #e9ecef;
    margin-bottom: 5px;
    border-radius: 5px;
}


// script.js
let timer = 0;
let interval;
let running = false;

const timeDisplay = document.getElementById("time");
const lapsList = document.getElementById("laps");

function formatTime(ms) {
    const totalSeconds = Math.floor(ms / 1000);
    const minutes = Math.floor(totalSeconds / 60);
    const seconds = totalSeconds % 60;
    const milliseconds = ms % 1000;
    return `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}:${String(Math.floor(milliseconds / 10)).padStart(2, "0")}`;
}

function startTimer() {
    if (!running) {
        running = true;
        const start = Date.now() - timer;
        interval = setInterval(() => {
            timer = Date.now() - start;
            timeDisplay.textContent = formatTime(timer);
        }, 10);
    }
}

function pauseTimer() {
    if (running) {
        running = false;
        clearInterval(interval);
    }
}

function resetTimer() {
    pauseTimer();
    timer = 0;
    timeDisplay.textContent = "00:00:00";
    lapsList.innerHTML = "";
}

function recordLap() {
    const lapTime = document.createElement("li");
    lapTime.textContent = formatTime(timer);
    lapsList.appendChild(lapTime);
}

document.getElementById("start").addEventListener("click", startTimer);
document.getElementById("pause").addEventListener("click", pauseTimer);
document.getElementById("reset").addEventListener("click", resetTimer);
timeDisplay.addEventListener("click", recordLap);

<!DOCTYPE html>
<html>
<head>
      <title>My project 3!</title>\
</head>



<body>
    <h1>My project!</h1>
    <p>My new web</p>
    <p><a href="http://127.0.0.1:5500/timer/timer.html">Click here </a> to check my timer</p> 
    <p><a href="http://127.0.0.1:5500/calendar.html">Click here </a> to check my calendar</p> 
    </body>
    </html>

    const monthYearDisplay = document.getElementById('month-year');
const calendarContainer = document.getElementById('calendar');

let currentDate = new Date();

function renderCalendar() {
  const currentMonth = currentDate.getMonth();
  const currentYear = currentDate.getFullYear();

  monthYearDisplay.textContent = `${getMonthName(currentMonth)} ${currentYear}`;

  calendarContainer.innerHTML = '';

  const firstDayOfMonth = new Date(currentYear, currentMonth, 1);
  const lastDayOfMonth = new Date(currentYear, currentMonth + 1, 0);
  const startingDay = firstDayOfMonth.getDay();
  const totalDays = lastDayOfMonth.getDate();

  for (let i = 0; i < startingDay; i++) {
    const dayElement = document.createElement('div');
    dayElement.classList.add('day');
    calendarContainer.appendChild(dayElement);
  }

  for (let i = 1; i <= totalDays; i++) {
    const dayElement = document.createElement('div');
    dayElement.classList.add('day');
    dayElement.textContent = i;
    calendarContainer.appendChild(dayElement);
  }
}

function prevMonth() {
  currentDate.setMonth(currentDate.getMonth() - 1);
  renderCalendar();
}

function nextMonth() {
  currentDate.setMonth(currentDate.getMonth() + 1);
  renderCalendar();
}

function getMonthName(monthIndex) {
  const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
  return months[monthIndex];
}

renderCalendar();

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Календарь</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="calendar-container">
    <div class="calendar-header">
      <button id="prev" onclick="prevMonth()">&lt;</button>
      <h2 id="month-year"></h2>
      <button id="next" onclick="nextMonth()">&gt;</button>
    </div>
    <div id="calendar" class="weekdays">
      <div class="weekdays">
        <div class="day">Monday</div>
        <div class="day">Tuesday</div>
        <div class="day">Wednesday</div>
        <div class="day">Thursday</div>
        <div class="day">Friday</div>
        <div class="day">Saturday</div>
        <div class="day">Sunday</div>
      </div>
      <div class="days"></div>
    </div>
  </div>
  <script src="index.js"></script>
</body>
</html>


.calendar-container {
    max-width: 400px;
    margin: 0 auto;
    font-family: Arial, sans-serif;
}

.calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 300px;
}

#calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 5px;
}

.day {
    padding: 5px;
    border: 1px solid #000000;
}

.day:hover {
    background-color: #2b00ff;
}


.days {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, auto);
    gap: 5px;
}

.day.empty {
    visibility: hidden;
}

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Timer</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>

<div id="timer"></div>

<script src="script.js"></script>
</body>
</html>


#timer {
    font-size: 48px;
    text-align: center;
    margin-top: 50px;
}



// Функция для форматирования времени в формат MM:SS
function formatTime(seconds) {
    let minutes = Math.floor(seconds / 60);
    seconds = seconds % 60;
    return `${minutes < 10 ? '0' : ''}${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
}

// Функция запускающая таймер
function startTimer(duration) {
    let timerDisplay = document.getElementById('timer');
    let timer = duration;
    let interval = setInterval(function () {
        timerDisplay.textContent = formatTime(timer);
        if (--timer < 0) {
            clearInterval(interval);
            timerDisplay.textContent = "Время вышло!";
        }
    }, 1000);
}

// Запуск таймера при загрузке страницы
window.onload = function () {
    startTimer(300); // Установите здесь нужное количество секунд для таймера
};

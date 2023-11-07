# courseproject-purejs-gamefrogger
Sample project using pure or vanila Javascript for Frogger game

### 1. Buatlah file index.html kemudian tulis kode berikut,
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Frogger</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>

    <h3>Seconds left: <span id="time-left">20</span></h3>
    <h3>Result: <span id="result"></span></h3>

    <button id="start-pause-button">Start/Pause</button>

    <div class="grid">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div class="ending-block"></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div class="log-left l1"></div>
        <div class="log-left l2"></div>
        <div class="log-left l3"></div>
        <div class="log-left l4"></div>
        <div class="log-left l5"></div>
        <div class="log-left l1"></div>
        <div class="log-left l2"></div>
        <div class="log-left l3"></div>
        <div class="log-left l4"></div>
        <div class="log-right l5"></div>
        <div class="log-right l1"></div>
        <div class="log-right l2"></div>
        <div class="log-right l3"></div>
        <div class="log-right l4"></div>
        <div class="log-right l5"></div>
        <div class="log-right l1"></div>
        <div class="log-right l2"></div>
        <div class="log-right l3"></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div class="car-left c1"></div>
        <div class="car-left c2"></div>
        <div class="car-left c3"></div>
        <div class="car-left c1"></div>
        <div class="car-left c2"></div>
        <div class="car-left c3"></div>
        <div class="car-left c1"></div>
        <div class="car-left c2"></div>
        <div class="car-left c3"></div>
        <div class="car-right c1"></div>
        <div class="car-right c2"></div>
        <div class="car-right c3"></div>
        <div class="car-right c1"></div>
        <div class="car-right c2"></div>
        <div class="car-right c3"></div>
        <div class="car-right c1"></div>
        <div class="car-right c2"></div>
        <div class="car-right c3"></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div class="starting-block frog"></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

### 2. Buatlah file style.css kemudian tulis kode berikut,
```
.grid {
    border: 1px solid black;
    height: 180px;
    width: 180px;
    display: flex;
    flex-wrap: wrap;
}

.grid div {
    height: 20px;
    width: 20px;
}

.ending-block {
    background-color: red;
}

.starting-block {
    background-color: blue;
}
.l1, .l2, .l3 {
    background-color: brown;
}

.l4, .l5 {
    background-color: lightblue;
}

.c1 {
    background-color: black;
}

.c2, .c3 {
    background-color: lightgrey;
}

.frog {
    background-color: green;
}
```

### 3. Buatlah file app.js kemudian tulis berikut,
```
const timeLeftDisplay = document.querySelector('#time-left')
const resultDisplay = document.querySelector('#result')
const startPauseButton = document.querySelector('#start-pause-button')
const squares = document.querySelectorAll('.grid div')
const logsLeft = document.querySelectorAll('.log-left')
const logsRight = document.querySelectorAll('.log-right')
const carsLeft = document.querySelectorAll('.car-left')
const carsRight = document.querySelectorAll('.car-right')

let currentIndex = 76
const width = 9
let timerId
let outcomeTimerId
let currentTime = 20

function moveFrog(e) {
    squares[currentIndex].classList.remove('frog')

    switch(e.key) {
        case 'ArrowLeft' :
             if (currentIndex % width !== 0) currentIndex -= 1
            break
        case 'ArrowRight' :
            if (currentIndex % width < width - 1) currentIndex += 1
            break
        case 'ArrowUp' :
            if (currentIndex - width >=0 ) currentIndex -= width
            break
        case 'ArrowDown' :
            if (currentIndex + width < width * width) currentIndex += width
            break
    }
    squares[currentIndex].classList.add('frog')
}

function autoMoveElements() {
    currentTime--
    timeLeftDisplay.textContent = currentTime
    logsLeft.forEach(logLeft => moveLogLeft(logLeft))
    logsRight.forEach(logRight => moveLogRight(logRight))
    carsLeft.forEach(carLeft => moveCarLeft(carLeft))
    carsRight.forEach(carRight => moveCarRight(carRight))
}

function checkOutComes() {
    lose()
    win()
}

function moveLogLeft(logLeft) {
    switch(true) {
        case logLeft.classList.contains('l1') :
            logLeft.classList.remove('l1')
            logLeft.classList.add('l2')
            break
        case logLeft.classList.contains('l2') :
            logLeft.classList.remove('l2')
            logLeft.classList.add('l3')
            break
        case logLeft.classList.contains('l3') :
            logLeft.classList.remove('l3')
            logLeft.classList.add('l4')
            break
        case logLeft.classList.contains('l4') :
            logLeft.classList.remove('l4')
            logLeft.classList.add('l5')
            break
        case logLeft.classList.contains('l5') :
            logLeft.classList.remove('l5')
            logLeft.classList.add('l1')
            break
    }
}

function moveLogRight(logRight) {
    switch(true) {
        case logRight.classList.contains('l1') :
            logRight.classList.remove('l1')
            logRight.classList.add('l5')
            break
        case logRight.classList.contains('l2') :
            logRight.classList.remove('l2')
            logRight.classList.add('l1')
            break
        case logRight.classList.contains('l3') :
            logRight.classList.remove('l3')
            logRight.classList.add('l2')
            break
        case logRight.classList.contains('l4') :
            logRight.classList.remove('l4')
            logRight.classList.add('l3')
            break
        case logRight.classList.contains('l5') :
            logRight.classList.remove('l5')
            logRight.classList.add('l4')
            break
    }
}

function moveCarLeft(carLeft) {
    switch(true) {
        case carLeft.classList.contains('c1') :
            carLeft.classList.remove('c1')
            carLeft.classList.add('c2')
            break
        case carLeft.classList.contains('c2') :
            carLeft.classList.remove('c2')
            carLeft.classList.add('c3')
            break
        case carLeft.classList.contains('c3') :
            carLeft.classList.remove('c3')
            carLeft.classList.add('c1')
            break
    }
}

function moveCarRight(carRight) {
    switch(true) {
        case carRight.classList.contains('c1') :
            carRight.classList.remove('c1')
            carRight.classList.add('c3')
            break
        case carRight.classList.contains('c2') :
            carRight.classList.remove('c2')
            carRight.classList.add('c1')
            break
        case carRight.classList.contains('c3') :
            carRight.classList.remove('c3')
            carRight.classList.add('c2')
            break
    }
}

function lose() {
    if (
        squares[currentIndex].classList.contains('c1') ||
        squares[currentIndex].classList.contains('l4') ||
        squares[currentIndex].classList.contains('l5') ||
        currentTime <= 0
    ) {
        resultDisplay.textContent = 'You lose!'
        clearInterval(timerId)
        clearInterval(outcomeTimerId)
        squares[currentIndex].classList.remove('frog')
        document.removeEventListener('keyup', moveFrog)
    }
}

function win() {
    if (squares[currentIndex].classList.contains('ending-block')) {
        resultDisplay.textContent = 'You Win!'
        clearInterval(timerId)
        clearInterval(outcomeTimerId)
        document.removeEventListener('keyup', moveFrog)
    }
}

startPauseButton.addEventListener('click', () => {
    if (timerId) {
        clearInterval(timerId)
        clearInterval(outcomeTimerId)
        outcomeTimerId = null
        timerId = null
        document.removeEventListener('keyup', moveFrog)
    } else {
        timerId = setInterval(autoMoveElements, 1000)
        outcomeTimerId = setInterval(checkOutComes, 50)
        document.addEventListener('keyup', moveFrog)
    }
})
```



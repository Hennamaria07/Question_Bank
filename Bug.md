# Bug Fix — Timer Not Starting
## Task

Fix the code so the timer starts counting seconds after clicking the button.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<p id="timer">0</p>
<button id="start">Start Timer</button>

<script>
let sec = 0;
document.getElementById("start").onclick = () => {
    setInterval(() => {
        sec = sec + 1;
        timer.innerHTML = seconds;
    }, 1000);
}
</script>

</body>
</html>
```
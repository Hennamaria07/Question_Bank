# Bug Fix — Clock Not Updating
## Task

Fix so digital clock shows correct current time every second.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<p id="clock"></p>

<script>
setInterval(() => {
    let now = new Date();
    clock.innerHTML = now.getHours + ":" + now.getMinutes();
}, 1000)
</script>

</body>
</html>
```
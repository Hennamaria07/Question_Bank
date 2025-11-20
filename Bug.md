## Bug Fix — Button Double Click Not Detecting
## Task

Fix the bug so double-clicking the button shows an alert.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<button id="btn">Double Click Me</button>

<script>
document.getElementById("btn").addEventListener("dbclick", function() {
    alert("Double clicked!");
});
</script>

</body>
</html>
```
# Bug Fix — Button Disable Not Working
## Task

Fix the bug where clicking "Disable" should disable the button.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<button id="main">Click Me</button>
<button id="disableBtn">Disable</button>

<script>
document.getElementById("disableBtn").onclick = function() {
    main.disable = true;
}
</script>

</body>
</html>
```
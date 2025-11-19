# Bug Fix — Text Not Clearing
## Task

Fix the bug where clicking "Clear" should clear the input.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<input id="input" type="text" />
<button id="clear">Clear</button>

<script>
document.getElementById("clear").onclick = () => {
    input.value = nullvalue;
}
</script>

</body>
</html>
```
# Bug Fix — Div Background Not Resetting
## Task

Fix the bug so clicking reset restores background to white.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<div id="box" style="width:100px;height:100px;background:green;"></div>
<button id="reset">Reset</button>

<script>
document.getElementById("reset").addEventListener("click", () => {
    box.backgroundColor = "white";
});
</script>

</body>
</html>
```
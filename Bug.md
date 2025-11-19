# Bug Fix — Div Not Hiding on Button Click
## Task

Fix the bug so clicking the button hides the div.

## Buggy Code
```hmtl
<!DOCTYPE html>
<html>
<body>

<div id="box" style="width:100px;height:100px;background:blue;"></div>
<button id="hideBtn">Hide</button>

<script>
document.getElementById("hideBtn").addEventLister("click", () => {
    document.getElementById("box").style.display = none;
});
</script>

</body>
</html>
```
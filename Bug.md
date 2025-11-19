# Bug Fix — Div Not Moving
## Task

Fix the bug where the box should move 10px right each time the button is clicked.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<div id="box" style="width:50px;height:50px;background:red;position:absolute;left:0px;"></div>
<button id="move">Move</button>

<script>
let pos = 0;
document.getElementById("move").onclick = function() {
    pos = pos + 10;
    document.getElementByID("box").style.left = pos + "pxs";
}
</script>

</body>
</html>
```
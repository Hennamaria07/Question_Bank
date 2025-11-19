# Bug Fix — Mouseover Event Not Triggering
## Task

Fix the bug so hovering over the box changes its color.

## Buggy Code
``` html <!DOCTYPE html>
<html>
<body>

<div id="box" style="width:100px;height:100px;background:gray;"></div>

<script>
document.getElementById("box").addEventListener("mousehover", function(){
    this.style.background = "yellow";
});
</script>

</body>
</html>
```
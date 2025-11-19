# Bug Fix — Text Color Change Not Working
## Task

Fix the bug so clicking the button should turn the text red.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<p id="t">Hello</p>
<button id="c">Change Color</button>

<script>
document.getElementById("c").addEventListener("click", function(){
    document.getElementById("t").style.color = red;
});
</script>

</body>
</html>
```
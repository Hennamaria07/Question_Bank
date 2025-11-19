# Bug Fix — Image Not Loading
## Task

Fix the code so the image loads when the button is clicked.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<img id="pic" width="200" />
<button id="load">Load Image</button>

<script>
document.getElementById("load").addEventListener("click", () => {
    pic.scr = "https://via.placeholder.com/200";
});
</script>

</body>
</html>
```
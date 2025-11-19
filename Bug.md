# Bug Fix — Image Toggle Not Working
## Task

Fix the bug so clicking toggles between two images.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<img id="img" src="https://via.placeholder.com/150" />
<button id="switch">Switch</button>

<script>
let toggle = false;
document.querySelector("#switch").addEventListen("click", () => {
    toggle = !toggle;
    img.src = toggle ? "img1.jpg" : "img2.jpg";
});
</script>

</body>
</html>
```
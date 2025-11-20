# Bug Fix — Image Not Rotating
## Task

Fix the bug so clicking the button rotates the image by 45 degrees each time.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<img id="img" src="https://via.placeholder.com/120" style="transition:0.3s;">
<button id="rot">Rotate</button>

<script>
let angle = 0;
rot.onclick = () => {
    angle =+ 45;
    img.style.tranform = "rotate(" + angle + "deg)";
}
</script>

</body>
</html>
```
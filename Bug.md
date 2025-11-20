# Bug Fix — Scroll to Top Not Working
## Task

Fix the bug so clicking the button scrolls smoothly to the top.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body style="height:2000px;">

<button id="top">Top</button>

<script>
document.getElementById("top").onclick = () => {
    window.ScrollTo({
        top: 0,
        behavior: "smooth"
    });
}
</script>

</body>
</html>
```
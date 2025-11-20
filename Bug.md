# Bug Fix — Hover Effect Not Removing
## Task

Fix so mouseout returns button to original color.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<button id="btn" style="background:blue;color:white;">Hover me</button>

<script>
btn.addEventListener("mouseover", () => {
    btn.style.background = "red";
});

btn.addEventListener("mouseoff", () => {
    btn.style.background = "blue";
});
</script>

</body>
</html>
```
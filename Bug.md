# Bug Fix — Paragraph Not Showing Length of Input
## Task

Fix so typing shows live character count.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input id="text">
<p id="len"></p>

<script>
text.addEventListener("input", () => {
    len.innerHTML = text.length;
});
</script>

</body>
</html>
```
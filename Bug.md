# Bug Fix — Checkbox Status Not Showing
## Task

Fix the bug so that checking the checkbox updates the message.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input type="checkbox" id="check">
<p id="status"></p>

<script>
document.getElementById("check").addEventListener("change", () => {
    status.innerHTML = check.checked ? "Checked" : "Uncheckedx";
});
</script>

</body>
</html>
```
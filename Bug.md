# Bug Fix — Radio Button Not Detecting Correct Value
## Task

Fix the bug so selecting a radio button shows the chosen gender.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input type="radio" name="g" value="Male"> Male
<input type="radio" name="g" value="Female"> Female
<p id="out"></p>

<script>
document.querySelectorAll("g").forEach(r => {
    r.addEventListener("change", () => {
        out.innerHTML = r.text;
    });
});
</script>

</body>
</html>
```
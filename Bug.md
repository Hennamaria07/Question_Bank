# Bug Fix — Text Not Changing on Dropdown
## Task

Fix the bug where selecting a color changes the text color.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<select id="color">
<option value="red">Red</option>
<option value="blue">Blue</option>
</select>

<p id="output">Color me</p>

<script>
document.getElementByID("color").addEvent("change", () => {
    output.style.color = this.value;
});
</script>

</body>
</html>
```
# Bug Fix — Input Value Not Updating
## Task

Fix the JavaScript bug where typing in the input should update the paragraph text live.

### Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input id="name" type="text" />
<p id="output"></p>

<script>
document.getElementById("name").onchange = () => {
    document.getElementById("output").innerHTML = name.value;
}
</script>

</body>
</html>
```
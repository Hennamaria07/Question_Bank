# Bug Fix — Password Show/Hide Not Working
## Task

Fix so clicking the icon shows/hides the password.

## Buggy Code
``` html 
<!DOCTYPE html>
<html>
<body>

<input id="pass" type="password">
<button id="toggle">Show</button>

<script>
toggle.onclick = () => {
    pass.type = pass.type === password ? "text" : "password";
}
</script>

</body>
</html>
```
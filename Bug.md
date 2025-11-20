# Bug Fix — Username Validation Not Working
## Task

Fix the bug where empty username should show "Username required".

## Buggy Code
```
<!DOCTYPE html>
<html>
<body>

<input id="u">
<button id="check">Check</button>
<p id="msg"></p>

<script>
check.onclick = () => {
    if(u.value == null){
        msg.innerHTML = "Username required";
    }
}
</script>

</body>
</html>
```
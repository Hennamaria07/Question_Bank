# Bug Fix — Alert Not Showing After 2 Seconds
## Task

Fix the bug so an alert shows after 2 seconds when clicking the button.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<button id="wait">Wait 2 sec</button>

<script>
document.getElementById("wait").onclick = function(){
    settimeout(() => {
        alert("Done!");
    }, 2000);
}
</script>

</body>
</html>
```
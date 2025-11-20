# Bug Fix — Wrong Sum Calculated
## Task

Fix so sum of two inputs shows correctly.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input id="a" type="number">
<input id="b" type="number">
<button id="sum">Sum</button>
<p id="res"></p>

<script>
document.getElementById("sum").onclick = () => {
    res.innerHTML = a + b;
}
</script>

</body>
</html>
```
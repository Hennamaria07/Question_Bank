# Bug Fix — Text Not Showing After Button Click
## Task

Fix the bug so clicking button displays the text typed in input.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<input id="i" type="text">
<button id="show">Show</button>
<p id="o"></p>

<script>
document.getElementById("show").onclick = () => {
    o.innerHTML = i.values;
}
</script>

</body>
</html>
```
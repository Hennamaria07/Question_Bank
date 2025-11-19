# Bug Fix — Counter Not Incrementing
## Task

Fix the bug where clicking "+" should increase the counter value.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<p id="count">0</p>
<button id="inc">+</button>

<script>
document.getElementByID("inc").onclick = function() {
    let num = document.getElementById("count").textContent;
    num++;
    document.getElementById("count").innerHTML = num;
}
</script>

</body>
</html>```
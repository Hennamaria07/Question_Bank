# Bug Fix — Simple Calculator Not Working
## Task

Fix so selecting the operator performs correct calculation.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<input id="x" type="number">
<select id="op">
<option value="+">+</option>
<option value="-">-</option>
</select>
<input id="y" type="number">
<button id="cal">Calculate</button>
<p id="res"></p>

<script>
cal.onclick = function() {
    if(op == "+") res.innerHTML = x.value + y.value;
    else res.innerHTML = x.value - y.value;
}
</script>

</body>
</html>
```
# Bug Fix — Text Not Reversing
## Task

Fix so clicking reverses the input string.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<input id="txt">
<button id="rev">Reverse</button>
<p id="out"></p>

<script>
rev.onclick = () => {
    out.innerHTML = txt.value.split("").reverse.join("");
}
</script>

</body>
</html>
```
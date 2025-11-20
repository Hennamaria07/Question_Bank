# Bug Fix — Form Validation Not Working
## Task

Fix so empty input shows an alert.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<form id="f">
<input id="n" type="text">
<button>Submit</button>
</form>

<script>
document.getElementById("f").onsubmit = (e) => {
    if(n.value = ""){
        alert("Required");
    }
}
</script>

</body>
</html>
```
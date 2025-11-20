# Bug Fix — Dark Mode Not Applying
## Task

Fix so clicking button toggles dark mode.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<button id="dark">Dark Mode</button>

<script>
document.getElementById("dark").addEventListener("click", function(){
    document.body.classlist.toggle("dark");
});
</script>

</body>
</html>
```
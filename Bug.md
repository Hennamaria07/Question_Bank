# Bug Fix — Background Color Toggle Not Working
## Task

Fix the bug where clicking the button should toggle the page's background color between white and black.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<button id="toggle">Toggle Theme</button>

<script>
let dark = false;
document.querySelector("#toggl").addEventListener("click", function(){
    dark = !dark;
    document.body.style.background = dark ? "black" : "white";
});
</script>

</body>
</html>
```
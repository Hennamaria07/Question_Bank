# Bug Fix — Background Color Picker Not Working
## Task

Fix so picking a color updates box background.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<input type="color" id="picker">
<div id="box" style="width:100px;height:100px;background:#ccc;"></div>

<script>
picker.addEventListener("input", () => {
    box.backgroud = picker.value;
});
</script>

</body>
</html>
```
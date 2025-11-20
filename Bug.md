# Bug Fix — Div Height Animation Not Working
## Task

Fix so clicking grows div height by animation.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<div id="box" style="width:100px;height:50px;background:orange;transition:height 0.5s;"></div>
<button id="grow">Grow</button>

<script>
grow.onclick = () => {
    box.hight = "200px";
}
</script>

</body>
</html>
```
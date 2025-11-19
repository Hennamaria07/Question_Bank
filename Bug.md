# Bug Fix — Dropdown Not Showing Selected Value
## Task

Fix the bug where the selected dropdown value should appear in the paragraph.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<select id="city">
  <option>Delhi</option>
  <option>Mumbai</option>
</select>

<p id="result"></p>

<script>
document.getElementById("city").addEventListener("change", function(){
    document.getElementById("result").innerText = city.val;
});
</script>

</body>
</html>
```
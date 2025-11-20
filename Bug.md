# Bug Fix — Remove Last List Item
## Task

Fix so clicking the button removes the last list item.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<ul id="list">
  <li>A</li>
  <li>B</li>
</ul>
<button id="rem">Remove Last</button>

<script>
rem.onclick = () => {
    list.removeChild(list.lastItem);
}
</script>

</body>
</html>
```
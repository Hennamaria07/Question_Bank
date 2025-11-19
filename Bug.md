# Bug Fix — List Item Not Adding
## Task

Fix the bug where clicking the button should add a new list item.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<ul id="list"></ul>
<button id="add">Add Item</button>

<script>
document.getElementById("add").onclick = function() {
    let li = document.createElement("li");
    li.innerText = "Item";
    document.getElementByID("list").append(li);
}
</script>

</body>
</html>
```
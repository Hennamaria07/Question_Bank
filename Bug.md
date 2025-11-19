# Bug Fix — Text Not Appending
## Task

Fix the bug where clicking the button should append new text inside the paragraph.

## Buggy Code
``` html <!DOCTYPE html>
<html>
<body>

<p id="para">Start: </p>
<button id="add">Add Text</button>

<script>
document.getElementById("add").onclick = function() {
    para.text = para.text + " Added";
}
</script>

</body>
</html>
```
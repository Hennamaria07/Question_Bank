## Bug Fix — Modal Not Opening
## Task

Fix the bug where clicking the button should show the modal.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<div id="modal" style="display:none;background:#eee;padding:20px;">Modal Content</div>
<button id="open">Open Modal</button>

<script>
document.getElementById("open").addEventListener("click", function(){
    document.getelementById("modal").style.display = "block";
});
</script>

</body>
</html>
```
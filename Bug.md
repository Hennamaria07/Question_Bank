# Bug Fix — Form Submission Prevent Default Not Working
## Task

Fix the bug so that form submission does NOT reload the page.

## Buggy Code
```html
<!DOCTYPE html>
<html>
<body>

<form id="myForm">
<input type="text" />
<button type="submit">Submit</button>
</form>

<script>
document.getElementById("myForm").submit = function(e) {
    e.preventDefault();
    alert("Form stopped!");
};
</script>

</body>
</html>
```
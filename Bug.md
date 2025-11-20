# Bug Fix — Audio Not Playing
## Task

Fix so clicking Play actually plays the audio.

## Buggy Code
``` html
<!DOCTYPE html>
<html>
<body>

<audio id="audio" src="song.mp3"></audio>
<button id="play">Play</button>

<script>
document.getElementByID("play").click = () => {
    audio.pla();
}
</script>

</body>
</html>
```
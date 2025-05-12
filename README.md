<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <style>
    body 
      {
       text-align: center;
       font-family: sans-serif;
       background-image: url('background.jpg');
       background-repeat: no-repeat;
      background-size: cover;   
      color:aliceblue;
      padding-top: 40px;
      }
    .grid 
    { 
      display: grid;
     grid-template-columns: repeat(3, 100px); 
     gap: 5px; margin: 20px auto; 
     width: max-content; 
    }
    .cell 
    { 
      width: 100px;
      height: 100px; 
      font-size: 2em; 
      border: 2px solid #11bac0; 
      display: flex; 
      align-items: center; 
      justify-content: center;
       cursor: pointer;
       }
    button
     {
       margin-top: 10px; 
       color:black;
       background-color: green;
       height:40px ;
       padding-left: 40px;
       padding-right: 30px;
       font-size: larger;
      }
      button:hover
      {
        background-color: rgb(81, 133, 4);
      }
</style>
</head>

<body>
<h2><span style="color:#007bff;">Tic Tac Toe</span> Vs <span style="color:#e91e63;">Computer</span></h2>
  <div class="grid" id="grid"></div>
  <div id="status">Your turn (X)</div>
  <button onclick="start()">Restart</button>

  <script>
    let grid = document.getElementById("grid");
    let status = document.getElementById("status");
    let board = Array(9).fill("");
    let gameOver = false;
    function start() {
      board.fill("");
      gameOver = false;
      status.textContent = "Your turn (X)";
      grid.innerHTML = "";
      board.forEach((_, i) => {
        let cell = document.createElement("div");
        cell.className = "cell";
        cell.onclick = () => playerMove(i);
        grid.appendChild(cell);
      });
    }
    function playerMove(i) {
      if (board[i] || gameOver) return;
      mark(i, "X");
      if (check("X")) return end("You win!");
      if (board.every(c => c)) return end("Draw!");
      setTimeout(computerMove, 300);
    }
    function computerMove() {
      let empty = board.map((v, i) => v ? null : i).filter(v => v !== null);
      let i = empty[Math.floor(Math.random() * empty.length)];
      mark(i, "O");
      if (check("O")) return end("Computer wins!");
      if (board.every(c => c)) return end("Draw!");
    }
    function mark(i, val) {
      board[i] = val;
      grid.children[i].textContent = val;
    }
    function check(p) {
      return [0,1,2,3,4,5,6,7,8].some((_, i, a) =>
        [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]]
        .some(c => c.every(x => board[x] === p))
      );
    }
    function end(msg) {
      status.textContent = msg;
      gameOver = true;
    }
    start();
  </script>
</body>
</html>

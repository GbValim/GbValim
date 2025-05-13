
## My Skills

#### Main Stack:
![Java](https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=java&logoColor=white)&nbsp;
![Eclipse](https://img.shields.io/badge/Eclipse-2C2255?style=for-the-badge&logo=eclipse&logoColor=white)&nbsp;

<img src="https://raw.githubusercontent.com/MicaelliMedeiros/micaellimedeiros/master/image/computer-illustration.png" min-width="400px" max-width="400px" width="400px" align="right" alt="Computador iuriCode">


#### Studying in this moment:

![Python](https://img.shields.io/badge/Python-FF0000?style=for-the-badge&logo=python&logoColor=white)&nbsp;
![React.js](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)&nbsp;





&nbsp;
&nbsp;

## Contacts:

<div> 
<a href="https://www.instagram.com/g4briel_v4lim" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white">
</a>
<a href = "mailto:contato.gabriel07mercury@gmail.com"> <img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
</div>&nbsp;&nbsp;
 

  
  
<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=8F0D87&height=120&section=footer"/>

<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Jogo da Cobrinha</title>
  <style>
    body {
      margin: 0;
      background-color: black;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    canvas {
      border: 2px solid #00ff00;
      background-color: black;
    }
  </style>
</head>
<body>
  <canvas id="game" width="400" height="400"></canvas>

  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");

    const gridSize = 20;
    const tileCount = canvas.width / gridSize;

    let snake = [{ x: 10, y: 10 }];
    let velocity = { x: 0, y: 0 };
    let food = {
      x: Math.floor(Math.random() * tileCount),
      y: Math.floor(Math.random() * tileCount)
    };
    let tail = 5;

    function gameLoop() {
      requestAnimationFrame(gameLoop);
      if (++temp < 5) return;
      temp = 0;

      ctx.fillStyle = "black";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      snake.push({
        x: snake[snake.length - 1].x + velocity.x,
        y: snake[snake.length - 1].y + velocity.y
      });

      while (snake.length > tail) snake.shift();

      // colisão com parede
      const head = snake[snake.length - 1];
      if (
        head.x < 0 || head.x >= tileCount ||
        head.y < 0 || head.y >= tileCount
      ) {
        resetGame();
        return;
      }

      // colisão com o próprio corpo
      for (let i = 0; i < snake.length - 1; i++) {
        if (snake[i].x === head.x && snake[i].y === head.y) {
          resetGame();
          return;
        }
      }

      // comida
      if (head.x === food.x && head.y === food.y) {
        tail++;
        food.x = Math.floor(Math.random() * tileCount);
        food.y = Math.floor(Math.random() * tileCount);
      }

      // desenhar a cobra
      ctx.fillStyle = "#00ff00";
      for (let s of snake) {
        ctx.fillRect(s.x * gridSize, s.y * gridSize, gridSize - 2, gridSize - 2);
      }

      // desenhar comida
      ctx.fillStyle = "#ff0000";
      ctx.fillRect(food.x * gridSize, food.y * gridSize, gridSize - 2, gridSize - 2);
    }

    function resetGame() {
      snake = [{ x: 10, y: 10 }];
      velocity = { x: 0, y: 0 };
      tail = 5;
    }

    document.addEventListener("keydown", e => {
      switch (e.key) {
        case "ArrowUp":
          if (velocity.y === 0) velocity = { x: 0, y: -1 };
          break;
        case "ArrowDown":
          if (velocity.y === 0) velocity = { x: 0, y: 1 };
          break;
        case "ArrowLeft":
          if (velocity.x === 0) velocity = { x: -1, y: 0 };
          break;
        case "ArrowRight":
          if (velocity.x === 0) velocity = { x: 1, y: 0 };
          break;
      }
    });

    let temp = 0;
    requestAnimationFrame(gameLoop);
  </script>
</body>
</html>


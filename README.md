<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Collect the Coins Game</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: Arial, sans-serif;
      background: linear-gradient(to bottom, #87ceeb, #ffffff);
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
<canvas id="gameCanvas"></canvas>

<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  // Player properties
  const player = {
    x: canvas.width / 2,
    y: canvas.height - 100,
    width: 50,
    height: 50,
    color: "blue",
    speed: 10
  };

  // Coin properties
  const coin = {
    x: Math.random() * (canvas.width - 30),
    y: Math.random() * (canvas.height - 150),
    width: 30,
    height: 30,
    color: "gold"
  };

  // Score
  let score = 0;

  // Draw player
  function drawPlayer() {
    ctx.fillStyle = player.color;
    ctx.fillRect(player.x, player.y, player.width, player.height);
  }

  // Draw coin
  function drawCoin() {
    ctx.fillStyle = coin.color;
    ctx.beginPath();
    ctx.arc(coin.x + coin.width / 2, coin.y + coin.height / 2, coin.width / 2, 0, Math.PI * 2);
    ctx.fill();
  }

  // Check collision
  function checkCollision() {
    if (
      player.x < coin.x + coin.width &&
      player.x + player.width > coin.x &&
      player.y < coin.y + coin.height &&
      player.y + player.height > coin.y
    ) {
      score++;
      resetCoin();
    }
  }

  // Reset coin position
  function resetCoin() {
    coin.x = Math.random() * (canvas.width - 30);
    coin.y = Math.random() * (canvas.height - 150);
  }

  // Display score
  function displayScore() {
    ctx.fillStyle = "black";
    ctx.font = "20px Arial";
    ctx.fillText(`Score: ${score}`, 20, 30);
  }

  // Game loop
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    drawPlayer();
    drawCoin();
    checkCollision();
    displayScore();

    requestAnimationFrame(gameLoop);
  }

  // Player movement
  window.addEventListener("keydown", (e) => {
    if (e.code === "ArrowLeft" && player.x > 0) {
      player.x -= player.speed;
    }
    if (e.code === "ArrowRight" && player.x + player.width < canvas.width) {
      player.x += player.speed;
    }
    if (e.code === "ArrowUp" && player.y > 0) {
      player.y -= player.speed;
    }
    if (e.code === "ArrowDown" && player.y + player.height < canvas.height) {
      player.y += player.speed;
    }
  });

  gameLoop();
</script>
</body>
</html>

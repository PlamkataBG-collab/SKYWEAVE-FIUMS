<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Snake Game with Restart</title>

  <style>
    :root {
      --font-sans: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      --color-text-primary: #ffffff;
      --color-text-tertiary: #a3a3a3;
      --color-border-secondary: #262626;
      --color-border-tertiary: #404040;
      --border-radius-lg: 12px;
      --border-radius-md: 6px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: #121212; color: var(--color-text-primary); }
    
    .wrap {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2rem 1rem;
      gap: 1.25rem;
      font-family: var(--font-sans);
    }
    .title {
      font-size: 13px;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--color-text-tertiary);
    }
    .game-frame {
      position: relative;
      border-radius: var(--border-radius-lg);
      overflow: hidden;
      border: 0.5px solid var(--color-border-secondary);
      background: #0a0a0a;
    }
    canvas { display: block; }
    .overlay {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 0.75rem;
      background: rgba(0,0,0,0.72);
      backdrop-filter: blur(2px);
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.2s;
    }
    .overlay.show { opacity: 1; pointer-events: all; }
    .overlay-title {
      font-size: 22px;
      font-weight: 500;
      color: #fff;
      letter-spacing: 0.04em;
    }
    .overlay-sub {
      font-size: 13px;
      color: rgba(255,255,255,0.5);
    }
    .btn-restart {
      margin-top: 0.5rem;
      padding: 9px 22px;
      font-size: 14px;
      font-weight: 500;
      background: transparent;
      color: #5DCAA5;
      border: 0.5px solid #5DCAA5;
      border-radius: var(--border-radius-md);
      cursor: pointer;
      letter-spacing: 0.03em;
      transition: background 0.15s, color 0.15s;
    }
    .btn-restart:hover { background: #5DCAA5; color: #0a0a0a; }
    .stats {
      display: flex;
      gap: 2rem;
      align-items: center;
    }
    .stat {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 2px;
    }
    .stat-label {
      font-size: 11px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--color-text-tertiary);
    }
    .stat-value {
      font-size: 22px;
      font-weight: 500;
      color: var(--color-text-primary);
      min-width: 2ch;
      text-align: center;
    }
    .divider {
      width: 0.5px;
      height: 32px;
      background: var(--color-border-tertiary);
    }
    .hint {
      font-size: 12px;
      color: var(--color-text-tertiary);
      letter-spacing: 0.04em;
    }
    .dot { display: inline-block; width: 6px; height: 6px; border-radius: 50%; background: #5DCAA5; margin-right: 6px; vertical-align: middle; }
  </style>
</head>
<body>

<div class="wrap">
  <span class="title">Snake</span>

  <div class="game-frame">
    <canvas id="game" width="400" height="400"></canvas>
    <div class="overlay" id="overlay">
      <div class="overlay-title" id="overlayTitle">Game Over</div>
      <div class="overlay-sub" id="overlaySub"></div>
      <button class="btn-restart" onclick="resetGame()">Play again</button>
    </div>
  </div>

  <div class="stats">
    <div class="stat">
      <span class="stat-label">Score</span>
      <span class="stat-value" id="scoreEl">0</span>
    </div>
    <div class="divider"></div>
    <div class="stat">
      <span class="stat-label">Best</span>
      <span class="stat-value" id="bestEl">0</span>
    </div>
  </div>

  <span class="hint"><span class="dot"></span>arrow keys to move</span>
</div>

<script>
  const canvas = document.getElementById("game");
  const ctx = canvas.getContext("2d");
  const scoreEl = document.getElementById("scoreEl");
  const bestEl = document.getElementById("bestEl");
  const overlay = document.getElementById("overlay");
  const overlaySub = document.getElementById("overlaySub");

  const gridSize = 20;
  const tileCount = canvas.width / gridSize;

  let snake, food, dx, dy, score, best = 0, gameOver, gameLoop;

  const SNAKE_COLOR = "#5DCAA5";
  const SNAKE_HEAD = "#9FE1CB";
  const FOOD_COLOR = "#D85A30";
  const GRID_COLOR = "rgba(255,255,255,0.025)";
  const BG = "#0a0a0a";

  function resetGame() {
    snake = [{ x: 10, y: 10 }];
    food = { x: 5, y: 5 };
    dx = 0;
    dy = 0;
    score = 0;
    gameOver = false;
    scoreEl.textContent = "0";
    overlay.classList.remove("show");
    
    clearTimeout(gameLoop);
    drawGame();
  }

  function drawGame() {
    if (gameOver) {
      if (score > best) {
        best = score;
        bestEl.textContent = best;
      }
      overlaySub.textContent = "Score: " + score;
      overlay.classList.add("show");
      return;
    }

    clearScreen();
    drawGrid();
    moveSnake();
    drawFood();
    drawSnake();
    checkCollision();

    gameLoop = setTimeout(drawGame, 100);
  }

  function clearScreen() {
    ctx.fillStyle = BG;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
  }

  function drawGrid() {
    ctx.strokeStyle = GRID_COLOR;
    ctx.lineWidth = 0.5;
    for (let x = 0; x <= canvas.width; x += gridSize) {
      ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, canvas.height); ctx.stroke();
    }
    for (let y = 0; y <= canvas.height; y += gridSize) {
      ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(canvas.width, y); ctx.stroke();
    }
  }

  function drawSnake() {
    snake.forEach((part, i) => {
      const isHead = i === 0;
      ctx.fillStyle = isHead ? SNAKE_HEAD : SNAKE_COLOR;
      ctx.fillRect(part.x * gridSize + 1, part.y * gridSize + 1, gridSize - 2, gridSize - 2);
    });
  }

  function moveSnake() {
    if (dx === 0 && dy === 0) return;

    const head = { x: snake[0].x + dx, y: snake[0].y + dy };
    snake.unshift(head);

    if (head.x === food.x && head.y === food.y) {
      score++;
      scoreEl.textContent = score;
      generateFood();
    } else {
      snake.pop();
    }
  }

  function drawFood() {
    ctx.fillStyle = FOOD_COLOR;
    ctx.fillRect(food.x * gridSize + 1, food.y * gridSize + 1, gridSize - 2, gridSize - 2);
  }

  function generateFood() {
    // Ensure food doesn't spawn on top of the snake
    let newFoodPos;
    let onSnake = true;
    
    while (onSnake) {
      newFoodPos = {
        x: Math.floor(Math.random() * tileCount),
        y: Math.floor(Math.random() * tileCount)
      };
      onSnake = snake.some(part => part.x === newFoodPos.x && part.y === newFoodPos.y);
    }
    food = newFoodPos;
  }

  function checkCollision() {
    const head = snake[0];
    
    // Walls
    if (head.x < 0 || head.y < 0 || head.x >= tileCount || head.y >= tileCount) {
      gameOver = true;
    }

    // Self
    for (let i = 1; i < snake.length; i++) {
      if (head.x === snake[i].x && head.y === snake[i].y) {
        gameOver = true;
      }
    }
  }

  window.addEventListener("keydown", e => {
    if(["ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].includes(e.code)) {
      e.preventDefault();
    }

    // Added safety check: Don't allow moving backwards into yourself if the snake is moving
    if (e.code === "ArrowUp" && dy !== 1) { dx = 0; dy = -1; }
    if (e.code === "ArrowDown" && dy !== -1) { dx = 0; dy = 1; }
    if (e.code === "ArrowLeft" && dx !== 1) { dx = -1; dy = 0; }
    if (e.code === "ArrowRight" && dx !== -1) { dx = 1; dy = 0; }
  });

  resetGame();
</script>
</body>
</html>

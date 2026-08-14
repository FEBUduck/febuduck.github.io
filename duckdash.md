---
layout: page
title: 🦆 Duck Dash 🦆
subtitle: Fans first. Ducks always.
---


# Duck Dash

# Duck Dash

<!-- GLOBAL FIXES: full‑screen, no scroll, stable player -->
<style>
  body, html {
    margin: 0;
    padding: 0;
    overflow: hidden;
  }

  #duckdash-game {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw !important;
    height: 100vh !important;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background: #003300;
    z-index: 9999;
  }

  #duckdash-player {
    pointer-events: none;
    position: absolute;
    width: 60px;
    height: 60px;
    bottom: 40px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 10000;
  }

  .duckdash-obstacle {
    position: absolute;
    width: 40px;
    height: 40px;
    background: #b5651d;
    border-radius: 5px;
  }

  #duckdash-score {
    position: absolute;
    top: 10px;
    left: 10px;
    font-size: 24px;
    color: white;
    font-family: Arial, sans-serif;
  }

  #duckdash-over {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 40px;
    color: white;
    display: none;
    font-family: Arial, sans-serif;
  }

  #duckdash-restart {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 20px;
    display: none;
  }
</style>

<div id="duckdash-game">
  <img id="duckdash-player" src="/assets/img/FEBUlogosmall.png">
  <div id="duckdash-score">Score: 0</div>
  <div id="duckdash-over">GAME OVER</div>
  <button id="duckdash-restart">Restart</button>
</div>

<script>
  const game = document.getElementById("duckdash-game");
  const player = document.getElementById("duckdash-player");
  const scoreDisplay = document.getElementById("duckdash-score");
  const gameOverText = document.getElementById("duckdash-over");
  const restartBtn = document.getElementById("duckdash-restart");

  let score = 0;
  let speed = 3;
  let obstacles = [];
  let alive = true;

  // Center player based on game div, not whole page
  let playerX = (game.offsetWidth / 2) - 30;
  const moveSpeed = 10;

  document.addEventListener("keydown", (e) => {
    if (!alive) return;

    if (e.key === "ArrowLeft" || e.key === "a") playerX -= moveSpeed;
    if (e.key === "ArrowRight" || e.key === "d") playerX += moveSpeed;

    player.style.left = playerX + "px";
  });

  function spawnObstacle() {
    if (!alive) return;

    const obs = document.createElement("div");
    obs.classList.add("duckdash-obstacle");

    // Spawn inside game div width
    obs.style.left = Math.random() * (game.offsetWidth - 40) + "px";
    obs.style.top = "-40px";

    game.appendChild(obs);
    obstacles.push(obs);
  }

  setInterval(spawnObstacle, 800);

  function loop() {
    if (!alive) return;

    obstacles.forEach((obs, index) => {
      let y = parseInt(obs.style.top);
      y += speed;
      obs.style.top = y + "px";

      const px = playerX;
      const py = game.offsetHeight - 100;

      const ox = parseInt(obs.style.left);
      const oy = y;

      // Collision detection
      if (
        ox < px + 60 &&
        ox + 40 > px &&
        oy < py + 60 &&
        oy + 40 > py
      ) {
        alive = false;
        gameOverText.style.display = "block";
        restartBtn.style.display = "inline-block";
      }

      // Off-screen cleanup
      if (y > game.offsetHeight) {
        obs.remove();
        obstacles.splice(index, 1);
        score++;
        scoreDisplay.textContent = "Score: " + score;
        speed += 0.05;
      }
    });

    requestAnimationFrame(loop);
  }

  loop();

  restartBtn.addEventListener("click", () => {
    location.reload();
  });
</script>

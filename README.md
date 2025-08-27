<!DOCTYPE html>
<html lang="fi">
<head>
  <meta charset="UTF-8">
  <title>Painopeli</title>
  <style>
    body { margin: 0; font-family: sans-serif; background: #f0f8ff; text-align: center; }
    #score, #time { font-size: 24px; margin: 10px; }
    #gameArea { position: relative; width: 100%; height: 80vh; background: #e0f7fa; overflow: hidden; }
    .btn { position: absolute; padding: 15px; border-radius: 10px; color: white; font-weight: bold; cursor: pointer; }
  </style>
</head>
<body>
  <h1>Painopeli</h1>
  <div id="score">Pisteet: 0</div>
  <div id="time">Aika: 30s</div>
  <div id="gameArea"></div>

  <script>
    const gameArea = document.getElementById('gameArea');
    let score = 0;
    let time = 30;

    function createButton() {
      const btn = document.createElement('div');
      btn.className = 'btn';
      btn.style.backgroundColor = `hsl(${Math.random()*360}, 70%, 50%)`;
      btn.innerText = Math.random() < 0.2 ? 'BONUS!' : 'PAINA!';
      const size = 80;
      const x = Math.random() * (gameArea.clientWidth - size);
      const y = Math.random() * (gameArea.clientHeight - size);
      btn.style.left = x + 'px';
      btn.style.top = y + 'px';
      btn.onclick = () => {
        score += btn.innerText === 'BONUS!' ? 3 : 1;
        document.getElementById('score').innerText = 'Pisteet: ' + score;
        gameArea.removeChild(btn);
        createButton();
      };
      gameArea.appendChild(btn);
    }

    function startGame() {
      createButton();
      const timer = setInterval(() => {
        time--;
        document.getElementById('time').innerText = 'Aika: ' + time + 's';
        if(time <= 0) {
          clearInterval(timer);
          alert('Aika loppui! Pisteesi: ' + score);
          location.reload();
        }
      }, 1000);
    }

    startGame();
  </script>
</body>
</html>

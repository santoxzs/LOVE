<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Para o amor da minha vida</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: 'Arial', sans-serif;
      background: #000;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      min-height: 100vh;
      text-align: center;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .container {
      z-index: 10;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 20px;
      backdrop-filter: blur(8px);
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .polaroid {
      background: white;
      padding: 20px 20px 60px 20px;
      border-radius: 15px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 0 30px rgba(255,255,255,0.5);
      cursor: pointer;
      transition: transform 0.3s;
    }

    .polaroid:hover {
      transform: scale(1.03);
    }

    .polaroid img {
      width: 100%;
      border-radius: 10px;
    }

    .caption {
      margin-top: 15px;
      font-size: 16px;
      color: #333;
      font-weight: bold;
    }

    .text-below {
      margin-top: 40px;
      font-size: 20px;
      color: white;
      max-width: 800px;
      padding: 0 20px;
      line-height: 1.6;
    }
  </style>
</head>
<body>

<canvas id="heartCanvas"></canvas>

<div class="container">
  <div class="polaroid" onclick="togglePhoto()">
    <img id="photo" src="https://i.postimg.cc/HVxrX9W2/pretoebranco.jpg" alt="Foto do casal">
    <div class="caption">clique na foto e veja a mágica ✨</div>
  </div>
  <div class="text-below">
    você na minha vida é tão especial assim como o impala é especial para o Dean, você chegou na minha vida e a mudou por completo, meus dias passaram a ter mais cor e a minha vida passou a ser mais feliz, não pude comprar um presente mas fiz isso para você. saiba que eu te amo muito meu amor da minha vida 🩷✨️
  </div>
</div>

<script>
  const canvas = document.getElementById('heartCanvas');
  const ctx = canvas.getContext('2d');
  let hearts = [];
  let miniExplosions = [];

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }

  window.addEventListener('resize', resize);
  resize();

  function createHeart(x = Math.random() * canvas.width, y = -20, size = 10 + Math.random() * 20, speed = 1 + Math.random() * 3) {
    return {
      x,
      y,
      size,
      speed,
      alpha: 0.5 + Math.random() * 0.5,
      explode: false,
    };
  }

  function drawHeart(x, y, size, alpha) {
    ctx.save();
    ctx.translate(x, y);
    ctx.scale(size / 30, size / 30);
    ctx.beginPath();
    ctx.moveTo(0, 0);
    ctx.bezierCurveTo(0, -3, -5, -15, -15, -15);
    ctx.bezierCurveTo(-35, -15, -35, 10, -35, 10);
    ctx.bezierCurveTo(-35, 25, -20, 40, 0, 50);
    ctx.bezierCurveTo(20, 40, 35, 25, 35, 10);
    ctx.bezierCurveTo(35, 10, 35, -15, 15, -15);
    ctx.bezierCurveTo(5, -15, 0, -3, 0, 0);
    ctx.closePath();
    ctx.fillStyle = `rgba(255, 105, 180, ${alpha})`;
    ctx.fill();
    ctx.restore();
  }

  function createMiniHearts(x, y) {
    const miniHearts = [];
    for (let i = 0; i < 15; i++) {
      miniHearts.push({
        x,
        y,
        size: 5 + Math.random() * 5,
        speedX: (Math.random() - 0.5) * 4,
        speedY: (Math.random() - 0.5) * 4,
        alpha: 1,
        life: 60
      });
    }
    return miniHearts;
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // adicionar corações
    if (Math.random() < 0.3) {
      hearts.push(createHeart());
    }

    // desenhar e mover corações
    hearts.forEach((heart, i) => {
      heart.y += heart.speed;
      drawHeart(heart.x, heart.y, heart.size, heart.alpha);

      if (heart.y > canvas.height) hearts.splice(i, 1);
    });

    // desenhar mini explosões
    miniExplosions.forEach((group, groupIndex) => {
      group.forEach((mini, i) => {
        mini.x += mini.speedX;
        mini.y += mini.speedY;
        mini.alpha -= 0.02;
        mini.life--;
        drawHeart(mini.x, mini.y, mini.size, mini.alpha);

        if (mini.life <= 0) {
          group.splice(i, 1);
        }
      });

      if (group.length === 0) {
        miniExplosions.splice(groupIndex, 1);
      }
    });

    requestAnimationFrame(animate);
  }

  // Função para criar e explodir 4 corações
  function explodeBigHearts() {
    for (let i = 0; i < 4; i++) {
      const x = Math.random() * canvas.width * 0.9 + 20;
      const y = Math.random() * canvas.height * 0.5 + 50;

      // desenha o coração grande (explosivo)
      drawHeart(x, y, 35, 1);
      miniExplosions.push(createMiniHearts(x, y));
    }
  }

  // chama a função de explosão a cada 5 segundos
  setInterval(explodeBigHearts, 5000);

  animate();

  let isColor = false;
  function togglePhoto() {
    const photo = document.getElementById("photo");
    if (!isColor) {
      photo.src = "https://i.postimg.cc/s11zJ6Sv/colorida.jpg";
    } else {
      photo.src = "https://i.postimg.cc/HVxrX9W2/pretoebranco.jpg";
    }
    isColor = !isColor;
  }
</script>
<div style="position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); z-index: 10; text-align: center;">
  <a href="https://open.spotify.com/track/2QjOHCTQ1Jl3zawyYOpxh6?si=1WfTbEetS4efBHymh8n-gw" target="_blank" style="background-color: #1DB954; color: white; padding: 10px 20px; text-decoration: none; border-radius: 30px; font-weight: bold; font-family: sans-serif; box-shadow: 0 4px 15px rgba(0,0,0,0.3); transition: background 0.3s;">
    🎧 Ouvir no Spotify
  </a>
</div>
</body>
</html>

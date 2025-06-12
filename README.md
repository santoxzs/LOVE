<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Para minha criança</title>
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

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }

  window.addEventListener('resize', resize);
  resize();

  function createHeart(x = Math.random() * canvas.width, y = -20, size = 20 + Math.random() * 30, speed = 1 + Math.random() * 2) {
    return {
      x,
      y,
      size,
      speed,
      alpha: 0.5 + Math.random() * 0.5,
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

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // adicionar corações continuamente
    if (Math.random() < 0.7) {
      hearts.push(createHeart());
    }

    // desenhar e mover corações
    hearts.forEach((heart, i) => {
      heart.y += heart.speed;
      drawHeart(heart.x, heart.y, heart.size, heart.alpha);

      if (heart.y > canvas.height) hearts.splice(i, 1);
    });

    requestAnimationFrame(animate);
  }

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

</body>
</html>

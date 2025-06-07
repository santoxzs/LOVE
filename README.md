<!DOCTYPE html>
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
      height: 100vh;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .container {
      text-align: center;
      z-index: 10;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.15);
      border-radius: 20px;
      backdrop-filter: blur(8px);
    }

    .polaroid {
      background: white;
      padding: 10px 10px 40px 10px;
      border-radius: 10px;
      width: 300px;
      box-shadow: 0 0 20px rgba(255,255,255,0.5);
      cursor: pointer;
      transition: transform 0.3s;
    }

    .polaroid:hover {
      transform: scale(1.05);
    }

    .polaroid img {
      width: 100%;
      border-radius: 5px;
    }

    .caption {
      margin-top: 10px;
      font-size: 14px;
      color: #333;
      font-weight: bold;
    }

    .text-below {
      margin-top: 30px;
      font-size: 18px;
      color: white;
      max-width: 600px;
      padding: 0 20px;
    }

    .hint {
      font-size: 14px;
      margin-top: 10px;
      color: #ffb6c1;
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

  function createHeart() {
    return {
      x: Math.random() * canvas.width,
      y: -20,
      size: 10 + Math.random() * 20,
      speed: 1 + Math.random() * 3,
      alpha: 0.5 + Math.random() * 0.5
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
    if (Math.random() < 0.3) {
      hearts.push(createHeart());
    }
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

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Valentine 💘</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', Arial, sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
    }

    .card {
      background: white;
      padding: 30px;
      border-radius: 20px;
      width: 90%;
      max-width: 420px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    }

    button {
      border: none;
      padding: 15px 25px;
      border-radius: 30px;
      font-size: 18px;
      cursor: pointer;
    }

    .next-btn { background: #ff5e78; color: white; }
    .yes-btn { background: #4CAF50; color: white; font-size: 22px; }
    .no-btn { background: #ccc; font-size: 12px; }

    img {
      width: 100%;
      border-radius: 20px;
      margin-top: 15px;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
    }
  </style>
</head>

<body>

<canvas id="confetti"></canvas>

<div class="card" id="step1">
  <h1>Hey Tarani 💕</h1>
  <p>These last couple of months have been one of the best.</p>
  <button class="next-btn" onclick="nextStep()">Next ➡️</button>
</div>

<div class="card" id="step2" style="display:none;">
  <h2>Will you be my Valentine? 💘</h2>
  <button class="yes-btn" onclick="sayYes()">YES 😍</button>
  <button class="no-btn" id="noBtn" onclick="noOption()">no</button>
  <p id="noText"></p>
</div>

<div class="card" id="step3" style="display:none;">
  <h2>Can't believe this beautiful lady is my Valentine 💖</h2>
  <img src="valentine.jpg">
</div>

<script>
  function nextStep() {
    step1.style.display = 'none';
    step2.style.display = 'block';
  }

  function noOption() {
    noBtn.style.display = 'none';
    noText.innerText = "Do you think you have an option? 😌 Hit the YES button please.";
  }

  function sayYes() {
    step2.style.display = 'none';
    step3.style.display = 'block';
    startConfetti();
  }

  const canvas = document.getElementById('confetti');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  let confetti = [];

  function startConfetti() {
    for (let i = 0; i < 120; i++) {
      confetti.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 6 + 4,
        d: Math.random() * 4 + 4,
        color: `hsl(${Math.random() * 360}, 100%, 50%)`
      });
    }
    requestAnimationFrame(drawConfetti);
  }

  function drawConfetti() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    confetti.forEach(c => {
      ctx.beginPath();
      ctx.fillStyle = c.color;
      ctx.arc(c.x, c.y, c.r, 0, Math.PI * 2);
      ctx.fill();
      c.y += c.d;
      if (c.y > canvas.height) c.y = -10;
    });
    requestAnimationFrame(drawConfetti);
  }
</script>

</body>
</html>

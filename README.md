<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Be My Valentine?</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: Arial, Helvetica, sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    .wrap {
      padding: 20px;
      width: 100%;
      max-width: 420px;
      z-index: 2;
    }

    .card {
      background: white;
      border-radius: 20px;
      padding: 30px 25px;
      text-align: center;
      box-shadow: 0 15px 40px rgba(0,0,0,0.15);
    }

    .title {
      font-size: 1.8rem;
      margin-bottom: 10px;
    }

    .subtitle {
      font-size: 1rem;
      color: #444;
      margin-bottom: 25px;
    }

    .buttons {
      position: relative;
      height: 120px;
    }

    .btn {
      font-size: 1.1rem;
      padding: 12px 24px;
      border: none;
      border-radius: 999px;
      cursor: pointer;
      position: absolute;
      transition: transform 0.2s;
    }

    .btn:active {
      transform: scale(0.95);
    }

    .btn-yes {
      background: #ff4d6d;
      color: white;
      left: 50%;
      top: 65px;
      transform: translateX(-50%);
    }

    .btn-no {
      background: #eee;
      color: #333;
      left: 50%;
      top: 10px;
      transform: translateX(-50%);
    }

    /* Floating hearts */
    .heart {
      position: absolute;
      bottom: -30px;
      font-size: 20px;
      animation: floatUp linear infinite;
      opacity: 0.8;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0);
        opacity: 1;
      }
      to {
        transform: translateY(-110vh);
        opacity: 0;
      }
    }

    /* Confetti */
    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: red;
      top: -10px;
      animation: confettiFall linear forwards;
    }

    @keyframes confettiFall {
      to {
        transform: translateY(110vh) rotate(360deg);
        opacity: 0;
      }
    }
  </style>
</head>

<body>
  <main class="wrap">
    <div class="card" id="card" aria-live="polite">
      <h1 class="title">Marco 💕</h1>
      <p class="subtitle">
        I think you’re wonderful. I’d be honored if you’d say yes —
        but I will always respect your choice.
      </p>

      <h2>Will you be my Valentine?</h2>

      <div class="buttons">
        <button id="yesBtn" class="btn btn-yes">Yes 💖</button>
        <button id="noBtn" class="btn btn-no">No</button>
      </div>
    </div>
  </main>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const card = document.getElementById("card");

    /* Make No button run away */
    noBtn.addEventListener("mouseover", () => {
      const x = Math.random() * 240;
      const y = Math.random() * 80;
      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
    });

    /* Floating hearts */
    function createHeart() {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.innerHTML = "❤️";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.animationDuration = 4 + Math.random() * 3 + "s";
      heart.style.fontSize = 14 + Math.random() * 20 + "px";
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), 7000);
    }

    setInterval(createHeart, 400);

    /* Confetti */
    function launchConfetti() {
      for (let i = 0; i < 120; i++) {
        const confetti = document.createElement("div");
        confetti.className = "confetti";
        confetti.style.left = Math.random() * 100 + "vw";
        confetti.style.backgroundColor =
          ["#ff4d6d", "#ffd166", "#4cc9f0", "#f72585"][
            Math.floor(Math.random() * 4)
          ];
        confetti.style.animationDuration = 2 + Math.random() * 3 + "s";
        document.body.appendChild(confetti);

        setTimeout(() => confetti.remove(), 5000);
      }
    }

    /* Yes click */
    yesBtn.addEventListener("click", () => {
      launchConfetti();
      card.innerHTML = `
        <h1 class="title">YAY MARCO 💖</h1>
        <p class="subtitle">
          I’m so happy you said yes 🥰<br><br>
          Happy Valentine’s Day ❤️
        </p>
      `;
    });
  </script>
</body>
</html>

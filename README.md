# valentine-quiz
A valentine's suprise 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Valentine Quiz 💘</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="box">
        <h1>💖 Welcome to My Quiz 💖</h1>
        <div id="score">Score: 0</div>
        <div id="question"></div>
        <div id="options"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background: pink;
    text-align: center;
    overflow-x: hidden;
}

.box {
    background: white;
    width: 90%;
    max-width: 500px;
    margin: 50px auto;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0 20px rgba(0,0,0,0.2);
}

button {
    padding: 10px 15px;
    margin: 10px;
    border-radius: 10px;
    border: none;
    background: red;
    color: white;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background: darkred;
}

/* floating hearts */
.heart {
    position: fixed;
    font-size: 20px;
    animation: float 6s linear;
    pointer-events: none;
}

@keyframes float {
    0% {transform: translateY(0);}
    100% {transform: translateY(-100vh);}
}
let score = 0, qIndex = 0;

const questions = [
  {
    q: "When did I first fall for you? 💘",
    options: ["Sep 26 – Aakriti Inauguration", "Nov 1 – Kerala Piravi", "Nov 13 – During proposal", "I don't remember 😌"],
    answer: sep 26
  },
  {
    q: "Who loves more 😘",
    options: ["Abjikuttan", "Aamimol", "Aamimol loves more", "Aamimol loves more and moreeeeeee"],
    answer: 4
  },
  {
    q: "Who is more cute 🥺",
    options: ["Abjikuttan", "One and only Abjikuttan", "Abjikuttan is more cute", "Abjikuttan is more and more cuteeeee"],
    answer: 4
  },
  {
    q: "How long are we staying together?",
    options: ["Forever", "Forever+Forever", "Infinity", "Infinity+Forever"],
    answer: 4
  },
  {
    q: "Who gets angry first 🥹?",
    options: ["Abjin", "Abjikuttan", "Andikannan", "Andikannan gets angry more and moreee"],
    answer: 4
  }
];

function loadQuestion() {
  if(qIndex < questions.length){
    document.getElementById("question").innerHTML = "<h3>" + questions[qIndex].q + "</h3>";
    let opts = "";
    questions[qIndex].options.forEach((opt, i) => {
      opts += `<button onclick="checkAnswer(${i})">${opt}</button>`;
    });
    document.getElementById("options").innerHTML = opts;
  } else finalQuestion();
}

function checkAnswer(i) {
  if(i === questions[qIndex].answer){
    score++; 
    document.getElementById("score").innerText = "Score: " + score;
  } else {
    score = Math.max(0, score-1);
    document.getElementById("score").innerText = "Score: " + score;
    alert("Ok wrong ans, u owe me a hug 😘");
  }
  qIndex++; 
  loadQuestion();
}

function finalQuestion() {
  document.getElementById("question").innerHTML = "<h2>💘 Abjikuttan 💘</h2><h3>Will you be my Valentine? 🥹❤️</h3>";
  document.getElementById("options").innerHTML = '<button onclick="yes()">YES 💕</button><button onclick="no()">NO 😌</button>';
}

function yes() {
  document.querySelector(".box").innerHTML = `
    <h1>💖 YAYYYYY 💖</h1>
    <img src="YOUR_PERSONAL_PHOTO_URL_HERE" alt="You and me" style="width:200px; border-radius:20px; margin:10px;">
    <p>Thank you for being mine and Happy Valentine's Day 💌</p>
    <p>Aamimol love you more more more 🫶</p>
    <p>Every heartbeat whispers your name 🫶</p>
    <p>Forever yours, no returns, no refunds 😘</p>
    <h2>💞💞💞</h2>
    <canvas id="confetti"></canvas>
  `;
  launchConfetti();
}

function no() {
  alert("Invalid choice ❌ System detected that you are already my Valentine 😏💘");
}

// Floating hearts
setInterval(()=>{
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.innerHTML = "💖";
  heart.style.left = Math.random()*100 + "vw";
  document.body.appendChild(heart);
  setTimeout(()=>heart.remove(),6000);
},500);

// Confetti effect
function launchConfetti(){
  const canvas = document.getElementById('confetti');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  
  const confettiPieces = [];
  for(let i=0; i<200; i++){
    confettiPieces.push({
      x: Math.random()*canvas.width,
      y: Math.random()*canvas.height-100,
      r: Math.random()*6+2,
      d: Math.random()*10+2,
      color: `hsl(${Math.random()*360}, 100%, 50%)`,
      tilt: Math.random()*10-10,
      tiltAngle: 0,
      tiltAngleIncrement: Math.random()*0.07+0.05
    });
  }
  
  function draw(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    confettiPieces.forEach(p=>{
      ctx.beginPath();
      ctx.lineWidth = p.r;
      ctx.strokeStyle = p.color;
      ctx.moveTo(p.x+p.tilt+p.r/2, p.y);
      ctx.lineTo(p.x+p.tilt, p.y+p.tilt+ p.r/2);
      ctx.stroke();
      p.tiltAngle += p.tiltAngleIncrement;
      p.y += (Math.cos(p.d)+3+p.r/2)/2;
      p.x += Math.sin(p.tiltAngle);
      if(p.y > canvas.height){ p.y = -10; p.x = Math.random()*canvas.width; }
    });
    requestAnimationFrame(draw);
  }
  draw();
}

loadQuestion();


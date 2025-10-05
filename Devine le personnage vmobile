<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Comics Mobile</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Bangers&display=swap');

  body {
    font-family: 'Bangers', cursive;
    background: #111;
    color: #fff;
    text-align: center;
    margin: 0;
    padding: 15px;
    transition: background 0.6s ease;
  }

  h1 {
    color: #ffeb3b;
    text-shadow: 3px 3px #f00;
    font-size: clamp(28px, 6vw, 42px);
    margin-bottom: 20px;
  }

  .quiz-box {
    background: #222;
    border: 4px solid yellow;
    border-radius: 15px;
    box-shadow: 0 0 20px red;
    padding: 20px;
    max-width: 95%;
    width: 400px;
    margin: auto;
  }

  .emoji {
    font-size: clamp(40px, 10vw, 70px);
    margin-bottom: 20px;
    transition: transform 0.3s ease, opacity 0.3s ease;
  }
  .emoji.pop { transform: scale(1.3); opacity: 1; }

  .quiz-box.shake { animation: shake 0.3s; }
  @keyframes shake {
    0%,100%{ transform: translateX(0);}
    25%{ transform: translateX(-10px);}
    75%{ transform: translateX(10px);}
  }

  input {
    padding: 15px;
    width: 85%;
    border-radius: 10px;
    border: none;
    font-size: 20px;
    text-align: center;
    margin-bottom: 10px;
    outline: none;
  }

  button {
    background: #ff4444;
    color: white;
    border: none;
    padding: 14px 25px;
    border-radius: 10px;
    font-size: 20px;
    cursor: pointer;
    margin-top: 5px;
    width: 85%;
    max-width: 250px;
    transition: 0.2s;
  }
  button:hover, button:active { background: #ff6666; transform: scale(1.05); }

  .timer {
    font-size: 22px;
    margin: 10px 0;
    color: #ffeb3b;
  }

  .score {
    font-size: 22px;
    margin-top: 15px;
    color: #00ff99;
  }

  .end-screen {
    display: none;
    padding: 20px;
  }

  .end-screen h2 {
    color: #ffeb3b;
    font-size: clamp(26px, 6vw, 38px);
  }

  @media (max-width: 600px) {
    .quiz-box {
      padding: 15px;
      border-width: 3px;
    }
  }
</style>
</head>
<body>

<h1>💥 QUIZ COMICS 💥</h1>

<!-- Sons -->
<audio id="sound-correct" src="https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg"></audio>
<audio id="sound-wrong" src="https://actions.google.com/sounds/v1/cartoon/wood_plank_flicks.ogg"></audio>
<audio id="sound-end" src="https://actions.google.com/sounds/v1/cartoon/metal_clang.ogg"></audio>

<div class="quiz-box" id="quiz">
  <div class="emoji" id="emoji">🕷️🕸️📸</div>
  <div class="timer" id="timer">⏱️ Temps : 10s</div>
  <input type="text" id="userAnswer" placeholder="Tape ta réponse ici..." autocomplete="off">
  <br>
  <button onclick="checkAnswer()">✅ Valider</button>
  <div class="score" id="score">Score : 0</div>
</div>

<div class="end-screen" id="end">
  <h2>🏆 Fin du quiz ! 🏆</h2>
  <p id="finalMessage"></p>
  <button onclick="restart()">🔁 Rejouer</button>
</div>

<script>
const questions = [
  { emojis: "🕷️🕸️📸", answer: "Spider-Man", color:"#d32f2f" },
  { emojis: "🛡️🇺🇸⭐", answer: "Captain America", color:"#1976d2" },
  { emojis: "🃏🤡💣", answer: "Joker", color:"#43a047" },
  { emojis: "🦇🌃💔", answer: "Batman", color:"#000000" },
  { emojis: "⚡🟥👊", answer: "Flash", color:"#ffeb3b" },
  { emojis: "👑🐆🌍", answer: "Black Panther", color:"#4a148c" },
  { emojis: "🦾💡🍷", answer: "Iron Man", color:"#ff5722" },
  { emojis: "🥒💪😡", answer: "Hulk", color:"#2e7d32" },
  { emojis: "🔨⚡🌩️", answer: "Thor", color:"#90caf9" },
  { emojis: "🎯👓🪓", answer: "Hawkeye", color:"#8e24aa" },
  { emojis: "🧙‍♀️🔮✨", answer: "Scarlet Witch", color:"#ad1457" }
];

// Mélange aléatoire
questions.sort(() => Math.random() - 0.5);

let current = 0;
let score = 0;
let timeLeft = 10;
let timerInterval;

function startTimer() {
  clearInterval(timerInterval);
  timeLeft = 10;
  document.getElementById("timer").innerText = `⏱️ Temps : ${timeLeft}s`;
  timerInterval = setInterval(() => {
    timeLeft--;
    document.getElementById("timer").innerText = `⏱️ Temps : ${timeLeft}s`;
    if(timeLeft <= 0) {
      clearInterval(timerInterval);
      nextQuestion(false);
    }
  }, 1000);
}

function animateEmoji() {
  const emoji = document.getElementById("emoji");
  emoji.classList.add("pop");
  setTimeout(() => emoji.classList.remove("pop"), 300);
}

function updateQuestion() {
  const q = questions[current];
  document.getElementById("emoji").innerText = q.emojis;
  document.body.style.background = q.color;
  document.getElementById("userAnswer").value = "";
  document.getElementById("userAnswer").focus();
  animateEmoji();
  startTimer();
}

function checkAnswer() {
  const input = document.getElementById("userAnswer").value.trim().toLowerCase();
  const correct = questions[current].answer.toLowerCase();
  clearInterval(timerInterval);
  const quizBox = document.getElementById("quiz");

  if(input === correct) {
    score++;
    document.getElementById("sound-correct").play();
  } else {
    document.getElementById("sound-wrong").play();
    quizBox.classList.add("shake");
    setTimeout(() => quizBox.classList.remove("shake"), 300);
  }
  nextQuestion();
}

function nextQuestion() {
  current++;
  if(current >= questions.length) {
    endQuiz();
    return;
  }
  document.getElementById("score").innerText = "Score : " + score;
  updateQuestion();
}

function endQuiz() {
  document.getElementById("sound-end").play();
  document.getElementById("quiz").style.display = "none";
  document.getElementById("end").style.display = "block";
  const msg = score === questions.length 
    ? "🔥 Parfait ! Tu es un vrai super-héros !" 
    : score >= questions.length / 2 
      ? "💪 Pas mal ! Tu as de vrais pouvoirs !" 
      : "😅 Tu ferais mieux d’appeler Alfred pour t’aider...";
  document.getElementById("finalMessage").innerText = `Ton score final : ${score}/${questions.length}\n${msg}`;
}

function restart() {
  score = 0;
  current = 0;
  questions.sort(() => Math.random() - 0.5);
  document.getElementById("end").style.display = "none";
  document.getElementById("quiz").style.display = "block";
  document.getElementById("score").innerText = "Score : 0";
  updateQuestion();
}

// Démarrage initial
updateQuestion();
</script>
</body>
</html>

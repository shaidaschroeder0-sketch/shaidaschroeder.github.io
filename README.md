
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Little Stars Learning</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #fff6d9;
  color: #352b52;
  text-align: center;
}
header {
  background: #7654d6;
  color: white;
  padding: 22px 12px;
}
header h1 { margin: 0; font-size: 30px; }
header p { margin-bottom: 0; }
main {
  width: 100%;
  max-width: 650px;
  margin: auto;
  padding: 18px;
}
.card {
  background: white;
  border-radius: 24px;
  padding: 22px 14px;
  margin: 12px 0;
  box-shadow: 0 4px 0 #eadffb;
}
h2 { font-size: 25px; }
.grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}
button {
  font-family: inherit;
  font-weight: bold;
  cursor: pointer;
  touch-action: manipulation;
}
.category {
  border: 3px solid #e5dcff;
  border-radius: 20px;
  background: #f7f2ff;
  padding: 16px 5px;
  font-size: 18px;
  min-height: 110px;
}
.category span {
  display: block;
  font-size: 38px;
  margin-bottom: 8px;
}
.category:active, .answer:active {
  transform: scale(.97);
}
#question {
  font-size: 25px;
  min-height: 60px;
}
#picture {
  font-size: 70px;
  margin: 10px;
}
.answers {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}
.answer {
  background: #e9f8ff;
  border: 3px solid #b9e7ff;
  border-radius: 18px;
  padding: 18px 6px;
  font-size: 23px;
  min-height: 76px;
}
.answer:disabled { cursor: default; }
#feedback {
  font-size: 20px;
  font-weight: bold;
  min-height: 28px;
  margin: 18px 0 8px;
}
#next {
  background: #7654d6;
  color: white;
  border: 0;
  border-radius: 16px;
  padding: 16px 24px;
  font-size: 20px;
  width: 100%;
}
#next:disabled { opacity: .45; }
#menu {
  background: #ffcf5a;
  border: 0;
  border-radius: 14px;
  padding: 12px 18px;
  font-size: 17px;
  margin-top: 12px;
}
#progress {
  height: 14px;
  border-radius: 20px;
  background: #eee8f8;
  overflow: hidden;
  margin: 12px 0;
}
#bar {
  height: 100%;
  width: 0;
  background: #48c79b;
  transition: width .2s;
}
.small { font-size: 15px; color: #655a78; }
.hidden { display: none; }
footer { padding: 15px; font-size: 14px; }
</style>
</head>
<body>

<header>
  <h1>⭐ Little Stars Learning ⭐</h1>
  <p>Play • Learn • Shine!</p>
</header>

<main>
  <section id="home" class="card">
    <div style="font-size:65px">🌈 🧸 🌟</div>
    <h2>Hello, Little Star!</h2>
    <p>Choose a game. Let's learn together!</p>
    <div class="grid">
      <button class="category" onclick="startGame('colours')">
        <span>🎨</span>Colours
      </button>
      <button class="category" onclick="startGame('numbers')">
        <span>🔢</span>Numbers
      </button>
      <button class="category" onclick="startGame('animals')">
        <span>🐶</span>Animals
      </button>
      <button class="category" onclick="startGame('letters')">
        <span>🔤</span>Letters
      </button>
      <button class="category" onclick="startGame('shapes')">
        <span>🔺</span>Shapes
      </button>
      <button class="category" onclick="startGame('food')">
        <span>🍎</span>Food
      </button>
    </div>
    <p class="small">For little learners aged 3–5</p>
  </section>

  <section id="play" class="card hidden">
    <p id="categoryName">Learning time!</p>
    <p>⭐ Stars: <strong id="score">0</strong></p>
    <p id="counter">Question 1 of 5</p>
    <div id="progress"><div id="bar"></div></div>
    <h2 id="question">Find the red colour!</h2>
    <div id="picture">🎨</div>
    <div id="answers" class="answers"></div>
    <div id="feedback" aria-live="polite">
      You can do it!
    </div>
    <button id="next" onclick="nextQuestion()" disabled>
      Next Question ➜
    </button>
    <button id="menu" onclick="showHome()">🏠 Game Menu</button>
  </section>

  <section id="finish" class="card hidden">
    <div style="font-size:70px">🏆</div>
    <h2>Amazing, Little Star!</h2>
    <p id="result" style="font-size:23px"></p>
    <p>You did a wonderful job learning today!</p>
    <button id="next" onclick="showHome()">🎮 Play Another Game</button>
  </section>
</main>

<footer>Made with love for little learners 💜</footer>

<script>
const games = {
  colours: [
    {q:"Find the red colour!",p:"🎨",a:"Red",c:["Blue","Red","Yellow","Green"]},
    {q:"What colour is the sun?",p:"☀️",a:"Yellow",c:["Purple","Blue","Yellow","Green"]},
    {q:"Find the blue colour!",p:"🌈",a:"Blue",c:["Red","Pink","Orange","Blue"]},
    {q:"What colour is grass?",p:"🌱",a:"Green",c:["Green","Purple","Red","Blue"]},
    {q:"Find the pink colour!",p:"🌸",a:"Pink",c:["Brown","Pink","Black","Green"]}
  ],
  numbers: [
    {q:"Which number is ONE?",p:"☝️",a:"1",c:["2","4","1","3"]},
    {q:"Count the apples!",p:"🍎 🍎",a:"2",c:["1","2","3","4"]},
    {q:"Which number is THREE?",p:"3️⃣",a:"3",c:["5","1","3","2"]},
    {q:"Count the stars!",p:"⭐ ⭐ ⭐ ⭐",a:"4",c:["2","4","1","3"]},
    {q:"Which number comes after 4?",p:"1, 2, 3, 4, ?",a:"5",c:["3","6","5","2"]}
  ],
  animals: [
    {q:"Which animal says woof?",p:"🐾",a:"Dog",c:["Cat","Dog","Fish","Cow"]},
    {q:"Which animal says meow?",p:"🐾",a:"Cat",c:["Duck","Dog","Cat","Sheep"]},
    {q:"Which animal gives us milk?",p:"🥛",a:"Cow",c:["Lion","Cow","Fish","Bird"]},
    {q:"Which animal can swim?",p:"💧",a:"Fish",c:["Fish","Cat","Chicken","Horse"]},
    {q:"Which animal has a long trunk?",p:"🌳",a:"Elephant",c:["Rabbit","Dog","Elephant","Frog"]}
  ],
  letters: [
    {q:"Find the letter A!",p:"🍎",a:"A",c:["B","A","C","D"]},
    {q:"Which letter starts Apple?",p:"🍎",a:"A",c:["E","O","A","M"]},
    {q:"Find the letter B!",p:"⚽",a:"B",c:["D","P","B","A"]},
    {q:"Which letter starts Cat?",p:"🐱",a:"C",c:["K","C","S","T"]},
    {q:"Find the letter M!",p:"🌙",a:"M",c:["N","W","M","L"]}
  ],
  shapes: [
    {q:"Find the circle!",p:"⭕",a:"Circle",c:["Square","Triangle","Circle","Star"]},
    {q:"Which shape has 3 sides?",p:"🔺",a:"Triangle",c:["Circle","Triangle","Square","Oval"]},
    {q:"Find the square!",p:"🟦",a:"Square",c:["Star","Circle","Square","Triangle"]},
    {q:"Which shape looks like a ball?",p:"⚽",a:"Circle",c:["Circle","Square","Triangle","Rectangle"]},
    {q:"Find the star shape!",p:"⭐",a:"Star",c:["Oval","Square","Star","Circle"]}
  ],
  food: [
    {q:"Which fruit is red?",p:"🍎",a:"Apple",c:["Banana","Apple","Pear","Lemon"]},
    {q:"Which fruit is yellow?",p:"🍌",a:"Banana",c:["Grape","Apple","Banana","Berry"]},
    {q:"Which food is a carrot?",p:"🥕",a:"Vegetable",c:["Fruit","Vegetable","Drink","Sweet"]},
    {q:"Which fruit grows in bunches?",p:"🍇",a:"Grapes",c:["Grapes","Carrot","Bread","Egg"]},
    {q:"What do we drink when thirsty?",p:"🥤",a:"Water",c:["Water","Sand","Paper","Shoes"]}
  ]
};

const names = {
  colours:"🎨 Colours",
  numbers:"🔢 Numbers",
  animals:"🐾 Animals",
  letters:"🔤 Letters",
  shapes:"🔺 Shapes",
  food:"🍎 Food"
};

let currentGame = [];
let questionIndex = 0;
let score = 0;
let answered = false;

function showHome() {
  document.getElementById("home").classList.remove("hidden");
  document.getElementById("play").classList.add("hidden");
  document.getElementById("finish").classList.add("hidden");
}

function startGame(category) {
  currentGame = [...games[category]];
  questionIndex = 0;
  score = 0;
  document.getElementById("home").classList.add("hidden");
  document.getElementById("finish").classList.add("hidden");
  document.getElementById("play").classList.remove("hidden");
  document.getElementById("categoryName").textContent = names[category];
  showQuestion();
}

function showQuestion() {
  answered = false;
  const q = currentGame[questionIndex];
  document.getElementById("score").textContent = score;
  document.getElementById("counter").textContent =
    "Question " + (questionIndex + 1) + " of " + currentGame.length;
  document.getElementById("bar").style.width =
    (questionIndex / currentGame.length * 100) + "%";
  document.getElementById("question").textContent = q.q;
  document.getElementById("picture").textContent = q.p;
  document.getElementById("feedback").textContent = "Tap your answer!";
  document.getElementById("next").disabled = true;

  const area = document.getElementById("answers");
  area.innerHTML = "";

  [...q.c].sort(() => Math.random() - 0.5).forEach(choice => {
    const button = document.createElement("button");
    button.className = "answer";
    button.textContent = choice;
    button.onclick = () => checkAnswer(choice, button);
    area.appendChild(button);
  });
}

function checkAnswer(choice, button) {
  if (answered) return;
  answered = true;

  const q = currentGame[questionIndex];
  const buttons = document.querySelectorAll(".answer");
  buttons.forEach(b => b.disabled = true);

  if (choice === q.a) {
    score++;
    document.getElementById("feedback").textContent =
      "🎉 Fantastic! You earned a star!";
    button.style.background = "#c9f8d7";
    button.style.borderColor = "#36a96b";
  } else {
    document.getElementById("feedback").textContent =
      "😊 Good try! The answer is " + q.a + ".";
    button.style.background = "#ffe0e0";
    button.style.borderColor = "#e99";
    buttons.forEach(b => {
      if (b.textContent === q.a) {
        b.style.background = "#c9f8d7";
        b.style.borderColor = "#36a96b";
      }
    });
  }

  document.getElementById("score").textContent = score;
  document.getElementById("bar").style.width =
    ((questionIndex + 1) / currentGame.length * 100) + "%";
  document.getElementById("next").disabled = false;
  document.getElementById("next").textContent =
    questionIndex === currentGame.length - 1
      ? "See My Stars! 🏆" : "Next Question ➜";
}

function nextQuestion() {
  if (!answered) return;

  questionIndex++;

  if (questionIndex >= currentGame.length) {
    document.getElementById("play").classList.add("hidden");
    document.getElementById("finish").classList.remove("hidden");
    document.getElementById("result").textContent =
      "You earned " + score + " out of " + currentGame.length + " stars! ⭐";
    return;
  }

  showQuestion();
}

showHome();
</script>
</body>
</html>


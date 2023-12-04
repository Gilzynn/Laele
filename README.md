<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jogo de Forca</title>
  <style>

    <script type="text/javascript"> var infolinks_pid = 3410510; var infolinks_wsid = 0; </script> <script type="text/javascript" src="//resources.infolinks.com/js/infolinks_main.js"></script>
    
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-bottom: 50px; /* Espaço para os anúncios */
    }

    h1 {
      color: #3498db;
    }

    button {
      font-size: 16px;
      margin: 20px;
      padding: 10px;
      cursor: pointer;
    }

    #keyboard {
      margin-top: 20px;
    }

    .used {
      color: red;
    }

    #ad-space {
      height: 50px; /* Altura do espaço destinado aos anúncios */
      background-color: #f2f2f2; /* Cor de fundo do espaço dos anúncios (pode ser ajustada) */
      margin-top: 20px; /* Espaço entre o jogo e os anúncios */
    }
  </style>
</head>
<body>

<!-- Página Inicial -->
<div id="initial-page">
  <h1>Bem-vindo ao Jogo de Forca</h1>
  <button onclick="startGame()">Iniciar Jogo</button>
</div>

<!-- Página do Jogo -->
<div id="game-page" style="display: none;">
  <h1>Jogo de Forca</h1>
  <div id="word-display"></div>
  <div id="wrong-letters"></div>
  <p>Pontuação: <span id="score">0</span></p>
  <div id="keyboard"></div>
  <button onclick="startGame()">Iniciar Novo Jogo</button>

  <!-- Espaço para Anúncios -->
  <div id="ad-space"></div>

  <button onclick="returnToHome()">Voltar para a Página Inicial</button>
</div>

<script>
  const words = ["javascript", "html", "css", "python", "java"];
  let selectedWord = "";
  let correctLetters = [];
  let wrongLetters = [];
  let score = 0;

  function startGame() {
    // Toggle display between pages
    document.getElementById("initial-page").style.display = "none";
    document.getElementById("game-page").style.display = "block";

    // Reset variables
    selectedWord = words[Math.floor(Math.random() * words.length)];
    correctLetters = [];
    wrongLetters = [];
    score = 0;

    // Display initial UI
    updateWordDisplay();
    updateWrongLetters();
    updateScoreDisplay();
    createKeyboard();

    // Event listener for key press
    document.addEventListener("keydown", handleKeyPress);
  }

  function updateWordDisplay() {
    const wordDisplay = document.getElementById("word-display");
    wordDisplay.innerHTML = selectedWord
      .split("")
      .map(letter => (correctLetters.includes(letter) ? letter : "_"))
      .join(" ");
  }

  function updateWrongLetters() {
    const wrongLettersDisplay = document.getElementById("wrong-letters");
    wrongLettersDisplay.textContent = `Letras Erradas: ${wrongLetters.join(", ")}`;
  }

  function updateScoreDisplay() {
    const scoreDisplay = document.getElementById("score");
    scoreDisplay.textContent = score;
  }

  function createKeyboard() {
    const keyboardDiv = document.getElementById("keyboard");
    keyboardDiv.innerHTML = "";
    const alphabet = "abcdefghijklmnopqrstuvwxyz";

    for (let letter of alphabet) {
      const button = document.createElement("button");
      button.textContent = letter.toUpperCase();
      button.addEventListener("click", () => handleKeyPress({ key: letter }));
      if (wrongLetters.includes(letter) || correctLetters.includes(letter)) {
        button.classList.add("used");
      }
      keyboardDiv.appendChild(button);
    }
  }

  function handleKeyPress(event) {
    const pressedKey = event.key.toLowerCase();
    if (selectedWord.includes(pressedKey)) {
      if (!correctLetters.includes(pressedKey)) {
        correctLetters.push(pressedKey);
        if (correctLetters.length === selectedWord.length) {
          score++;
          startGame();
        }
      }
    } else {
      if (!wrongLetters.includes(pressedKey)) {
        wrongLetters.push(pressedKey);
        if (wrongLetters.length === 6) {
          // Game over condition
          alert("Você perdeu! Tente novamente.");
          startGame();
        }
      }
    }

    updateWordDisplay();
    updateWrongLetters();
    updateScoreDisplay();
    createKeyboard();
  }

  function returnToHome() {
    // Toggle display between pages
    document.getElementById("initial-page").style.display = "block";
    document.getElementById("game-page").style.display = "none";
  }
</script>

</body>
</html>

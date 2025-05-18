---
layout: base 
title: Lab Simulation 2.0
search_exclude: true
permalink: /labsim2.0/
---

NOTE: THIS PAGE WILL ONLY WORK WITH THE JEKYLL MINIMA THEME, DOES NOT WORK WITH CAYMAN

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Science Trivia</title>
  <style>
    body {
        background: linear-gradient(150deg,rgba(255, 234, 0, 0.23),rgba(0, 13, 255, 0.18),rgba(179, 255, 160, 0.28));
        color:rgb(4, 2, 2);
        font-family: Arial, sans-serif;
        min-height: 100vh;
        margin: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow-y: auto;
    }
    .container {
        background: rgba(255, 255, 255, 0.1);
        padding: 30px;
        border-radius: 12px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        max-width: 500px;
        width: 100%;
        text-align: center;
    }
    h2, h3 {
        color: rgb(255, 255, 255);
        border-bottom: 4px solid #000000;
        padding: 10px;
        margin-bottom: 20px;
    }
    #options {
        display: flex;
        flex-direction: column;
        gap: 20px;
        margin-top: 20px;
    }
    .button {
        all: unset;
        background-color: white !important;
        border: 2px solid #ccc;
        border-radius: 12px;
        padding: 10px 20px;
        font-size: 16px;
        cursor: pointer;
        transition: background-color 0.3s ease, transform 0.1s ease;
        font-weight: bold;
        color: black !important;
        margin: 0 auto;
        width: 80%;
        text-align: center;
    }
    .button:hover {
        background-color: gray !important;
        transform: scale(1.05);
    }
    .button:active {
        background-color: darkgrey !important;
        transform: scale(0.95);
    }
    input {
        padding: 10px;
        width: 80%;
        margin-top: 10px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 8px;
    }
    #difficulty {
        color: white;
        font-size: 18px;
        font-weight: bold;
        margin-bottom: 10px;
    }
    .attempts-container {
        text-align: center;
        margin-top: 30px;
        color: white;
    }
    .attempts-list {
        list-style: none;
        padding: 0;
        margin: 0 auto;
        width: fit-content;
    }
    #playAgainButton {
        display: inline-block;
        margin-top: 55px;
        font-size: 18px;
        padding: 12px 25px;
        border-radius: 14px;
        margin-bottom: 10px;
    }
    #submitButton {
        display: inline-block;
        margin-top: 25px;
        font-size: 18px;
        padding: 12px 25px;
        border-radius: 14px;
        margin-bottom: 10px;
    }
  </style>
</head>
<body>

<div class="container" id="lab">
  <h2 id="scenario">Loading...</h2>
  <p id="difficulty"></p>
  <div id="options"></div>
  <div id="gameOver" style="display:none;">
    <h2>Game Over!</h2>
    <p id="score"></p>
    <p id="usernameDisplay"></p>
    <div id="previousAttemptsContainer" class="attempts-container"></div>
    <button id="playAgainButton" style="display:none;" onclick="restartLab()">Play Again</button>
  </div>
</div>

<script>
const fetchOptions = {
  credentials: 'include' // Include cookies for authentication
};
// Define the backend URI (similar to your previous implementation)
var pythonURI;
if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8887";
} else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8887";
} else {
        pythonURI =  "https://flocker.nighthawkcodingsociety.com";
}

let questions = [];
let currentDifficulty = 3;
let points = 0;
let correctStreak = 0;
let wrongStreak = 0;

// Fetch questions
async function fetchQuestions() {
  try {
    console.log("Fetching questions...");
    const response = await fetch(`${pythonURI}/api/questions`);
    if (!response.ok) {
      throw new Error(`Failed to fetch questions: ${response.status}`);
    }
    const data = await response.json();
    if (!Array.isArray(data) || data.length === 0) {
      throw new Error("No questions found in the response.");
    }
    questions = data.map(q => ({
      question: q.scenario,
      distractor1: q.options[1],
      distractor2: q.options[2],
      distractor3: q.options[0],
      correct_answer: q.answer,
      difficulty_rating: q.difficulty
    }));
    console.log("Questions fetched:", questions);
    loadQuestion();
  } catch (error) {
    console.error('Error fetching questions:', error);
    document.getElementById('scenario').textContent = "Hmm, the server seems to be down. Please try again later.";
  }
}

function getQuestionByDifficulty(difficulty) {
  const filtered = questions.filter(q => parseInt(q.difficulty_rating) === difficulty);
  return filtered[Math.floor(Math.random() * filtered.length)];
}

function loadQuestion() {
  console.log("Loading question...");
  const currentQuestion = getQuestionByDifficulty(currentDifficulty);
  console.log("Current question:", currentQuestion);

  if (!currentQuestion) {
    endLab();
    return;
  }

  document.getElementById('scenario').textContent = currentQuestion.question;
  document.getElementById('difficulty').textContent = `Difficulty Level: ${currentQuestion.difficulty_rating}`;
  const optionsDiv = document.getElementById('options');
  optionsDiv.innerHTML = '';

  const options = [
    currentQuestion.correct_answer,
    currentQuestion.distractor1,
    currentQuestion.distractor2,
    currentQuestion.distractor3
  ].sort(() => Math.random() - 0.5);

  options.forEach(option => {
    const button = document.createElement('button');
    button.textContent = option;
    button.classList.add('button');
    button.onclick = () => checkAnswer(option, currentQuestion.correct_answer);
    optionsDiv.appendChild(button);
  });
}

function endLab() {
  document.getElementById('scenario').textContent = "No more questions available.";
  document.getElementById('options').innerHTML = '';
}

function checkAnswer(selected, correct) {
  if (selected === correct) {
    points++;
    correctStreak++;
    wrongStreak = 0; // Reset wrong streak on a correct answer
    if (currentDifficulty < 5) currentDifficulty++;
    if (correctStreak === 3 && currentDifficulty === 5) {
      winGame();
      return;
    }
  } else {
    correctStreak = 0;
    if (currentDifficulty > 1) {
      currentDifficulty--; // Decrease difficulty
      wrongStreak = 0; // Reset wrong streak when difficulty changes
    } else {
      wrongStreak++; // Increment wrong streak only at difficulty level 1
      if (wrongStreak === 3) {
        loseGame();
        return;
      }
    }
  }
  loadQuestion();
}

// Global variables to store fetched data
let username = null;
let previousAttempts = [];

// Function to fetch the logged-in user's name from the 'posts' endpoint
async function fetchUsername() {
  try {
    const response = await fetch(`${pythonURI}/api/posts/filter`, {
      ...fetchOptions, // Use the defined fetchOptions
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ channel_id: channelId }) // Replace `channelId` with the appropriate value
    });
    if (!response.ok) throw new Error("Failed to fetch posts data");

    const postData = await response.json();
    if (postData.length > 0) {
      username = postData[0].user_name; // Extract the username from the first post
    } else {
      username = "Guest"; // Default fallback if no posts are found
    }
  } catch (error) {
    console.error("Error fetching username:", error);
    username = "Guest"; // Default fallback
  }
}

// Function to fetch previous attempts (points) from the 'labsim' endpoint
async function fetchPreviousAttempts() {
  try {
    const response = await fetch(`${pythonURI}/api/labsim`, {
      method: 'GET',
      credentials: 'include', // Include cookies for authentication
      headers: {
        'Content-Type': 'application/json'
      }
    });
    if (!response.ok) throw new Error("Failed to fetch previous attempts");

    const data = await response.json();
    previousAttempts = data.map(attempt => attempt.points); // Extract points from each attempt
  } catch (error) {
    console.error("Error fetching previous attempts:", error);
    previousAttempts = []; // Default fallback
  }
}

// Show game-over screen with username and previous attempts
function showGameOverScreen(message) {
  // Hide game elements
  document.getElementById('scenario').style.display = 'none';
  document.getElementById('options').style.display = 'none';

  // Show game-over screen
  document.getElementById('gameOver').style.display = 'block';
  document.getElementById('score').textContent = `Points: ${points}`;
  document.getElementById('usernameDisplay').textContent = `Username: ${username}`;

  // Display previous attempts
  const container = document.getElementById('previousAttemptsContainer');
  container.innerHTML = ''; // Clear previous content

  if (previousAttempts.length > 0) {
    const attemptsHTML = previousAttempts.map((attempt, i) => `<li>Attempt ${i + 1}: ${attempt} points</li>`).join('');
    container.innerHTML = `
        <h3>Previous Attempts for ${username}:</h3>
        <ul class="attempts-list">${attemptsHTML}</ul>
    `;
  } else {
    container.innerHTML = `<p>No previous attempts found.</p>`;
  }

  // Show the "Play Again" button
  document.getElementById('playAgainButton').style.display = 'inline-block';
}

// Win or lose logic
function winGame() {
  showGameOverScreen('You Win!');
}

function loseGame() {
  showGameOverScreen('Game Over!');
}

// Restart the game
function restartLab() {
  currentDifficulty = 3;
  points = 0;
  correctStreak = 0;
  wrongStreak = 0;
  document.getElementById('gameOver').style.display = 'none';
  document.getElementById('scenario').style.display = 'block';
  document.getElementById('options').style.display = 'block';
  document.getElementById('options').innerHTML = ''; // Clear options
  loadQuestion();
}

// Initialize the game
(async () => { 
  await fetchUsername(); // Fetch the logged-in user's name at startup
  await fetchPreviousAttempts(); // Fetch the user's previous attempts
  fetchQuestions(); // Start by fetching questions
})();

window.restartLab = restartLab;
</script>

</body>
</html>
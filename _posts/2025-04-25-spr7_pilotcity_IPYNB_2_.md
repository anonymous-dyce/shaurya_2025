---
layout: page
title: All Code From Sprint 7
categories: ['Previous Code']
toc: True
permalink: /labsim2.0/sprint7allcode
---

Notes:

- Fetching the username and their previous attempts was unsuccessful, find another way of fetching username now that 'posts' api and model is no longer available
- For first version, console responded with "Error fetching username: ReferenceError: channelId is not defined" for fetching username and "Error fetching previous attempts: Error: Failed to fetch previous attempts" for fetching previous attempts
- Add main.py code to a main.py file that you can run 
- Add frontend code to frontend file with repo running on jekyll minima (cayman does not work)

#### The project

- This was a part of our BioSKANZ project, a version of Scripps Research: Biotech Engagement Game Development by PilotCity
- Our goal was to develop an engaging, interactive online game that educates Scripps Research's social media followers about their groundbreaking biotech innovations, aiming to increase follower engagement by 30% within three months, with potential deliverables including a virtual lab simulation and a biotech trivia challenge."

# Frontend Code:

``` markdown

---
layout: base 
title: Lab Simulation 2.0
search_exclude: true
permalink: /labsim2.0/
---


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
```

# Backend API code:

```python

from flask import Blueprint, request, jsonify, current_app, Response, g
from flask_restful import Api, Resource  # Used for REST API building
from __init__ import app  # Ensure __init__.py initializes your Flask app
from model.labsim import LabSim
from api.jwt_authorize import token_required

# Blueprint for the API

labsim_api = Blueprint('labsim_api', __name__, url_prefix='/api')
api_labsim = Api(labsim_api)  # Attach Flask-RESTful API to the Blueprint
class LabSimAPI:
    class _CRUD(Resource):
        @token_required()
        def post(self):
            # Obtain the request data sent by the RESTful client API
            data = request.get_json()
            # Create a new post object using the data from the request
            post = LabSim(points=data['points'], name1=data['name1'])
            # Save the post object using the Object Relational Mapper (ORM) method defined in the model
            post.create()
            # Return response to the client in JSON format, converting Python dictionaries to JSON format
            return jsonify(post.read())

        @token_required()
        def put(self):
            data = request.get_json()
            if not data or not data.get("points") or not data.get("name1"):
                return jsonify({"message": "name and points are required to update"}), 400
            old = LabSim.query.filter_by(name1=data["name1"], points=data["points"]).first()
            if not old:
                return jsonify({"message": "name and points not found"}), 404

            # Update the object's attributes
            old.name1 = data["new_name1"]
            old.points = data["new_points"]
            if old.update():
                #return "hello"
                return jsonify({"message": "name and points updated", "old name1": data["name1"], "new_name1": old.name1, "old_points": data["points"], "new_points": old.points})
           # coolfact.update({"coolfacts": data["coolfacts"], "points": data["points"]})

        @token_required()
        def get(self):
            try:
                # Query all entries in the BinaryHistory table
                entries = LabSim.query.all()
                # Convert the entries to a list of dictionaries
                results = [entry.read() for entry in entries]
                # Return the list of results in JSON format
                return jsonify(results)
            except Exception as e:
                # Return an error message in case of failure
                return jsonify({"error": str(e)}), 500

        @token_required()
        def delete(self):
            # Obtain the request data
            data = request.get_json()
            # Find the current post from the database table(s)
            post = LabSim.query.get(data['id'])
            # Delete the post using the ORM method defined in the model
            post.delete()
            # Return response
            return jsonify({"message": "Post deleted"})

    api_labsim.add_resource(_CRUD, '/labsim')

if __name__ == '__main__':
    app.run(debug=True)

```

# Backend model code:

```python
from sqlite3 import IntegrityError
from sqlalchemy import Text
from __init__ import app, db
from model.user import User

class LabSim(db.Model):
    """
    Labsim Model
    
    The LabSim class represents an individual lab simulation attempt by a user.
    
    Attributes:
        id (db.Column): The primary key, an integer representing the unique identifier for the lab attempt.
        _name1 (db.Column): An integer representing the user who created the lab attempt (foreign key to users.id).
        _points (db.Column): A string representing the points scored in the lab attempt.
    """
    __tablename__ = 'labsim'

    id = db.Column(db.Integer, primary_key=True)
    _name1 = db.Column(db.Integer, db.ForeignKey('users.id'), nullable=False)
    _points = db.Column(db.String(255), nullable=False)

    def __init__(self, name1, points):
        """
        Constructor, 1st step in object creation.
        """
        self._name1 = name1
        self._points = points

    def __repr__(self):
        """
        The __repr__ method is a special method used to represent the object in a string format.
        Called by the repr(post) built-in function, where post is an instance of the LabSim class.
        
        Returns:
            str: A text representation of how to create the object.
        """
        return f"LabSim(id={self.id}, name1={self._name1}, points={self._points})"

    def read(self):
        """
        The read method retrieves the object data from the object's attributes and returns it as a dictionary.
        
        Uses:
            The User.query method to retrieve the user object.
        
        Returns:
            dict: A dictionary containing the lab simulation data, including the user's name.
        """
        user = User.query.get(self._name1)
        data = {
            "id": self.id,
            "user_name": user.name if user else None,  # Retrieve the user's name
            "points": self._points
        }
        return data
    
    def update(self):
        """
        The update method commits the transaction to the database.
        
        Uses:
            The db ORM method to commit the transaction.
        
        Raises:
            Exception: An error occurred when updating the object in the database.
        """
        try:
            db.session.commit()
        except Exception as e:
            db.session.rollback()
            raise e
    
    def delete(self):
        """
        The delete method removes the object from the database and commits the transaction.
        
        Uses:
            The db ORM methods to delete and commit the transaction.
        
        Raises:
            Exception: An error occurred when deleting the object from the database.
        """    
        try:
            db.session.delete(self)
            db.session.commit()
        except Exception as e:
            db.session.rollback()
            raise e

def initLabSim():
    """
    The initPosts function creates the Post table and adds tester data to the table.
    
    Uses:
        The db ORM methods to create the table.
    
    Instantiates:
        Post objects with tester data.
    
    Raises:
        IntegrityError: An error occurred when adding the tester data to the table.
    """        
    with app.app_context():
        """Create database and tables"""
        db.create_all()
        """Tester data for table"""
        
        p1 = LabSim(name1=1, points="1")  
        p2 = LabSim(name1=2, points="2")
        p3 = LabSim(name1=3, points="3")
        p4 = LabSim(name1=1, points="4")
        
        for post in [p1, p2, p3, p4]:
            try:
                post.create()
                print(f"Record created: {repr(post)}")
            except IntegrityError:
                '''fails with bad or duplicate data'''
                db.session.remove()
                print(f"Records exist, duplicate email, or error: {post.uid}")
```

# Backend code in main.py:

``` python

# Path to the CSV file
csv_file_path = os.path.join(os.path.dirname(__file__), 'test.csv')

# Load the CSV data into memory
def load_csv_data(file_path):
    data = []
    try:
        with open(file_path, newline='', encoding='utf-8') as csvfile:
            reader = csv.DictReader(csvfile)
            for row in reader:
                # Convert difficulty_rating to an integer
                row['difficulty_rating'] = int(row['difficulty_rating'])
                data.append(row)
    except Exception as e:
        print(f"Error loading CSV file: {e}")
    return data

# Load the data at startup
questions_data = load_csv_data(csv_file_path)

@app.route('/api/questions', methods=['GET'])
def get_questions():
    try:
        # Optional: Get the difficulty from query parameters
        difficulty = request.args.get('difficulty', type=int)

        # Filter questions by difficulty if provided
        if difficulty is not None:
            filtered_questions = [
                {
                    "scenario": row["question"],
                    "options": [row["distractor3"], row["distractor1"], row["distractor2"], row["correct_answer"]],
                    "answer": row["correct_answer"],
                    "difficulty": row["difficulty_rating"]
                }
                for row in questions_data if row["difficulty_rating"] == difficulty
            ]
            if not filtered_questions:
                return jsonify({'error': 'No questions found for the given difficulty'}), 404
            return jsonify(filtered_questions), 200

        # If no difficulty parameter is provided, return all questions
        all_questions = [
            {
                "scenario": row["question"],
                "options": [row["distractor3"], row["distractor1"], row["distractor2"], row["correct_answer"]],
                "answer": row["correct_answer"],
                "difficulty": row["difficulty_rating"]
            }
            for row in questions_data
        ]
        return jsonify(all_questions), 200

    except Exception as e:
        return jsonify({'error': str(e)}), 500
```

### Have test.csv in backend (without being in a folder) so that main.py can access it

---
layout: page
title: All Code From Sprint 4 and 5
search_exclude: True
toc: True
permalink: /blogs/4and5allcode/
categories: ['Previous Code']
---

## This was my frontend code:

``` markdown
---
layout: page
title: History of Binary
search_exclude: true
permalink: /binary_history/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary History</title>
    <style>
        body {
            background: linear-gradient(150deg, #0E3348, #247994, #147EA0, #0F547B);
            color: #ffffff;
            font-family: Arial, sans-serif;
            min-height: 100vh;
            margin: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-y: auto;
        }
        h2, h3 {
            color: rgb(0, 0, 0);
            border-bottom: 4px solid #000000;
            font-weight: bold; /* Bold text */
            text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.8),  /* White shadow */
                         2px 2px 0 rgba(255, 255, 255, 0.6); /* Lighter shadow */
            border-radius: 10px; /* Rounded effect */
            padding: 10px; /* Space around the text */
            margin-bottom: 20px
        }
        .event {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #000000;
            border-radius: 5px;
        }
        p {
            color: white 
        }
        table {
            width: 100%;
            text-align: center;
            border-collapse: separate;
            border-spacing: 10px;
            border: none; /* Remove any borders from the table */
        }
        td {
            background-color: transparent !important; /* Remove background color */
            padding: 0 !important; /* Remove padding */
            border: none !important; /* Remove borders from table cells */
        }
        div {
            margin: 20px 0;
        }
        textarea {
            height: 100px;
            width: 1000px;
        }
        .regularButton {
            all: unset; /* Removes all default styles */
            background-color: white !important;
            border: 2px solid #ccc;
            border-radius: 12px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.1s ease;
            font-weight: bold;
            color: black !important;
        }
        .regularButton:hover {
            background-color: gray !important; /* Light gray on hover */
            transform: scale(1.05);
        }
        .regularButton:active {
            background-color: darkgrey !important; /* Slightly darker gray when clicked */
            transform: scale(0.95); /* Slight scale-down effect on click */
        }
    </style>
</head>
<body>
    <div id="binary-history"></div>

<h2>Add a Binary History Event!</h2>
<p>Make sure it is appropriate and relevant to the topic, otherwise it will get deleted...</p>
<p>NOTE: It does not have to be directly related to binary, it can be related to one of the default events.</p>
<textarea placeholder="Enter the year" id="eventYear" style="height: 30px; width: 200px;"></textarea>
<p></p>
<textarea placeholder="Enter the event description here..." id="eventDescription"></textarea>
<p></p>
<button class="regularButton" onclick="addEvent()">Submit Event</button>
<p></p>
<button class="regularButton"><a href="{{site.baseurl}}/binary_history/blog">Check out my Blog!</a></button>
<p></p>
<button class="regularButton"><a href="{{site.baseurl}}/trialsPartners">Back to Game</a></button>

<script type="module" defer>
    import { pythonURI, fetchOptions } from '../assets/js/api/config.js';

    async function fetchAndDisplayBinaryHistory() { 
        try {
            fetch(pythonURI + "/api/binary-history", // Fetch binary history from the given URI
            {
                method: "GET", // Use GET method
                headers: {
                    "Content-Type": "application/json", // Set request headers
                }
            })
            .then(response => { // Handle the response
                if (response.ok) {
                    return response.json(); // Parse the JSON if the response is there
                }
                throw new Error("Network response failed"); // Handle error if response is not there
            })
            .then(data => { // Process the received data

                // Sort events from oldest year to newest year
                data.sort((a, b) => a.year - b.year);

                // Get the container where history will be displayed
                const historyContainer = document.getElementById('binary-history');

                // Clear any previous content
                historyContainer.innerHTML = '';

                // Display each event
                data.forEach((event) => { // Iterate through each event in the data
                    const eventDiv = document.createElement('div'); // Create a div for each event
                    eventDiv.classList.add('event'); // Add a class for styling

                    const title = document.createElement('h3'); // Create element for the year
                    title.textContent = event["year"]; // Set the year as text content

                    const description = document.createElement('p'); // Create element for description
                    description.textContent = event.description; // Set description as text content

                    eventDiv.appendChild(title); // Append title to the event div
                    eventDiv.appendChild(description); // Append description to the event div

                    historyContainer.appendChild(eventDiv); // Append the event div to the container
                });
            })
            .catch(error => { // Handle any errors during fetch
                console.error("There was a problem with the fetch", error);
            });
            
        } catch (error) { // Handle any errors during the function execution
            console.error('Error fetching binary history:', error);
        }
    }

    fetchAndDisplayBinaryHistory();
        
    async function addEvent() { // Define an async function to add an event
        const year = document.getElementById('eventYear').value.trim(); // Get year value from input
        const description = document.getElementById('eventDescription').value.trim(); 
        // Get description value from input

        if (!year || !description) {
            alert('Please fill in both the year and event description.'); // Alert if inputs are invalid
            return;
        }

        const eventData = { // Create an object with the event data
            year: parseInt(year, 10), // Parse year as an integer
            description: description, // Add description
        };

        try {
            fetch(pythonURI + "/api/binary-history", { // Send a POST request to add the event
                method: "POST", // Use POST method
                headers: {
                    "Content-Type": "application/json", // Set request headers
                },
                body: JSON.stringify(eventData) // Send event data in the body of the request
            })
            .then(response => { // Handle the response
                if (response.ok) {
                    alert("Saved successfully!"); // Check if the response is there
                    return response.json(); // Parse the JSON if response is there
                }
                throw new Error("Network response failed"); // Handle error if response is not there
            })
            .then(data => { // Process the response data
                document.getElementById('eventYear').value = ''; // Clear the input fields
                document.getElementById('eventDescription').value = '';
                fetchAndDisplayBinaryHistory(); // Refresh the displayed history
            })
            .catch(error => { // Handle any errors during fetch
                console.error("There was a problem with the fetch", error);
            });

        } catch (error) { // Handle any errors during the function execution
            console.error('Error fetching binary history:', error);
        }
    }

    window.addEvent = addEvent; // Assign the addEvent function to the global scope
</script>
</body>
</html>
```



## This was my API code:

``` python
from flask import Blueprint, request, jsonify, current_app, Response, g
from flask_restful import Api, Resource  # Used for REST API building
from __init__ import app  # Ensure __init__.py initializes your Flask app
from model.binaryhistory import BinaryHistory

# Blueprint for the API
binary_history_api = Blueprint('binary_history_api', __name__, url_prefix='/api')

api = Api(binary_history_api)  # Attach Flask-RESTful API to the Blueprint

class BinaryHistoryAPI:
    """
    Define the API CRUD endpoints for the Post model.
    There are four operations that correspond to common HTTP methods:
    - post: create a new post
    - get: read posts
    - put: update a post
    - delete: delete a post
    """
    class _CRUD(Resource):
        def get(self):
            try:
                # Query all entries in the BinaryHistory table
                entries = BinaryHistory.query.all()
                # Convert the entries to a list of dictionaries
                results = [entry.read() for entry in entries]
                # Return the list of results in JSON format
                return jsonify(results)
            except Exception as e:
                # Return an error message in case of failure
                return jsonify({"error": str(e)}), 500
        
        def post(self):
            # Obtain the request data sent by the RESTful client API
            data = request.get_json()
            # Create a new post object using the data from the request
            post = BinaryHistory(data['year'], data['description'])
            # Save the post object using the Object Relational Mapper (ORM) method defined in the model
            post.create()
            # Return response to the client in JSON format, converting Python dictionaries to JSON format
            return jsonify(post.read())
        
        def put(self):
            # Obtain the request data
            data = request.get_json()
            # Find the current post from the database table(s)
            post = BinaryHistory.query.get(data['id'])
            # Update the post
            post.year = data['year']
            post.description = data['description']
            # Save the post
            post.update()
            # Return response
            return jsonify(post.read())

        
        def delete(self):
            # Obtain the request data
            data = request.get_json()
            # Find the current post from the database table(s)
            post = BinaryHistory.query.get(data['id'])
            # Delete the post using the ORM method defined in the model
            post.delete()
            # Return response
            return jsonify({"message": "Post deleted"})

    """
    Map the _CRUD class to the API endpoints for /post.
    - The API resource class inherits from flask_restful.Resource.
    - The _CRUD class defines the HTTP methods for the API.
    """
    api.add_resource(_CRUD, '/binary-history')
    
if __name__ == '__main__':
    app.run(debug=True)
```

## This was my model code:

``` python
from sqlite3 import IntegrityError
from sqlalchemy.exc import SQLAlchemyError
from __init__ import app, db

class BinaryHistory (db.Model):
    """
    BinaryHistory Model
    Represents an event with the year and description associated.
    """
    __tablename__ = 'binaryHistory'

    id = db.Column(db.Integer, primary_key=True)
    year = db.Column(db.String(255), nullable=False)
    description = db.Column(db.String(255), nullable=False)

    def __init__(self, year, description):
        """
        Constructor for BinaryHistory.
        """
        self.year = year
        self.description = description

    def __repr__(self):
        """
        Represents the BinaryHistory object as a string for debugging.
        """
        return f"<BinaryHistory(id={self.id}, year='{self.year}', description='{self.description})>"

    def create(self):
        """
        Adds the event to the database and commits the transaction.
        """
        try:
            db.session.add(self)
            db.session.commit()
        except SQLAlchemyError as e:
            db.session.rollback()
            raise e

    def read(self):
        """
        Returns the event details as a dictionary.
        """
        return {
            "id": self.id,
            "year": self.year,
            "description": self.description,
        }

    def update(self, data):
        """
        Updates the event with new data and commits the changes.
        """
        for key, value in data.items():
            if hasattr(self, key):
                setattr(self, key, value)
        try:
            db.session.commit()
        except SQLAlchemyError as e:
            db.session.rollback()
            raise e

    def delete(self):
        """
        Deletes the event from the database and commits the transaction.
        """
        try:
            db.session.delete(self)
            db.session.commit()
        except SQLAlchemyError as e:
            db.session.rollback()
            raise e
    
    @staticmethod
    def restore(data):
        """
        Restores data into the binaryHistory table from a given list of dictionaries.
        If an event with the same description and year exists, it skips adding or updates it.
        Args:
            data (list of dict): List of dictionaries with "year" and "description".
        """
        restored_count = 0
        skipped_count = 0

        for item in data:
            year = item.get("year")
            description = item.get("description")
            
            # Check if both fields are provided
            if not year or not description:
                print(f"Invalid data: {item}")
                continue
            
            # Check if the record already exists in the database
            existing_event = BinaryHistory.query.filter_by(year=year, description=description).first()
            
            if existing_event:
                print(f"Skipped: {existing_event}")
                skipped_count += 1
                continue
            
            # Add a new record if it doesn't exist
            try:
                new_event = BinaryHistory(year=year, description=description)
                db.session.add(new_event)
                db.session.commit()
                print(f"Restored: {new_event}")
                restored_count += 1
            except SQLAlchemyError as e:
                db.session.rollback()
                print(f"Failed to restore: {item}, Error: {e}")
        
        print(f"Restored: {restored_count}, Skipped: {skipped_count}")

def initBinaryHistory():
    """
    Initializes the binaryHistory table and inserts test data for development purposes.
    """
    with app.app_context():
        db.create_all()  # Create the database and tables

        # Sample test data
        events = [
            BinaryHistory(description="Gottfried Wilhelm Leibniz conceives the idea of the binary numeral system in his essay 'Explication de l'Arithmétique Binaire'.", year="1679"),
            BinaryHistory(description="Leibniz formally publishes his work on the binary numeral system in 'Explication de l'Arithmétique Binaire'.", year="1703"),
            BinaryHistory(description="George Boole develops Boolean algebra, which becomes foundational for binary logic.", year="1847"),
            BinaryHistory(description="George Boole publishes 'An Investigation of the Laws of Thought', further detailing Boolean algebra.", year="1854"),
            BinaryHistory(description="Claude Shannon applies Boolean algebra to design electronic circuits in his master's thesis.", year="1937"),
            BinaryHistory(description="John Atanasoff and Clifford Berry create the Atanasoff-Berry Computer (ABC), which uses binary.", year="1939"),
            BinaryHistory(description="John von Neumann outlines the architecture of modern computers, emphasizing binary.", year="1945"),
            BinaryHistory(description="The ENIAC computer is completed, though it uses decimal rather than binary.", year="1946"),
            BinaryHistory(description="Claude Shannon publishes 'A Mathematical Theory of Communication', linking binary to information theory.", year="1948"),
            BinaryHistory(description="Alan Turing's work on binary-based computation contributes to the development of modern computer science.", year="1950"),
            BinaryHistory(description="The UNIVAC I, the first commercial computer, uses binary in its operations.", year="1951"),
            BinaryHistory(description="Binary-coded decimal (BCD) becomes widely adopted for numerical representation in computing.", year="1960"),
            BinaryHistory(description="ASCII (American Standard Code for Information Interchange) is introduced, using binary to represent characters.", year="1964"),
            BinaryHistory(description="The UNIX operating system is created, relying heavily on binary representations.", year="1969"),
            BinaryHistory(description="Intel releases the 4004 microprocessor, the first commercially available processor based on binary.", year="1971"),
            BinaryHistory(description="IBM introduces the PC, making binary-based computing accessible to the public.", year="1980"),
            BinaryHistory(description="The World Wide Web is introduced, built upon binary protocols and systems.", year="1991"),
            BinaryHistory(description="The Y2K problem highlights the importance of binary in year representation and storage.", year="2000"),
            BinaryHistory(description="Bitcoin, based on binary and cryptographic principles, is introduced.", year="2008")
        ]

# to add to the database via postman, run main.py, go to postman, then select post, body, and then raw
# enter this link next to the post method: http://127.0.0.1:8887/api/binary-history
# in the blank body, enter data in JSON format, here is an example (based off the data above):
# {"description": "Quantum computing advancements begin to challenge traditional binary systems with qubits.", "year": "2020"}

        # Add each event to the database
        for event in events:
            try:
                db.session.add(event)  # Add the event to the session
                db.session.commit()
            except IntegrityError:
                db.session.rollback()
                print(f"Record already exists or error occurred: {event}")
```

How to properly make your site dynamic:
- Add the api and model files within the api and model folder, respectively
- Add the following things in main.py (in their proper places):
``` python
from api.binaryhistory import binary_history_api
from model.binaryhistory import BinaryHistory, initBinaryHistory
app.register_blueprint(binary_history_api)
#def generate_data():
    initBinaryHistory()
```
- When you run scripts/db_init.py in the database, it should make the database and have BinaryHistory, as well as its data, show up
- Run main.py and check for any errors; afterward, go on Postman and do the following:
    - Select "GET" from the dropdown and enter this link into the textbox: http://127.0.0.1:{host-domain}/api/binary-history
    - Select "POST", enter the same link, and below it, select "body", "raw", and enter the following: {"description": "Quantum computing advancements begin to challenge traditional binary systems with qubits.", "year": "2025"}
- If everything so far worked, your backend works perfectly
- Now, make a new file in your frontend and paste the frontend code along with styling if you want to have it
- Make the file and you should see your page appear when you enter the permalink! If nothing is showing or the output doesnt work or show properly, check the console log for errors through CTRL+SHIFT+J -> console before asking AI or debugging

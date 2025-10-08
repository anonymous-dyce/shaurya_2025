---
layout: page
title: Tri 2 Final Exam Blog - Write-up Blog
search_exclude: True
toc: True
permalink: /blogs/t2fbwriteup
categories: ["Shaurya's Blogs"]
---

#### Input and Output:

``` javascript
    <textarea placeholder="Enter the year" id="eventYear" style="height: 30px; width: 200px;"></textarea>
    <p></p>
    <textarea placeholder="Enter the event description here..." id="eventDescription"></textarea>
    <p></p>
    <button class="regularButton" onclick="addEvent()">Submit Event</button>
```

- This is where the user enters an event related to the history of binary
- They can enter the year and description of the event, which aligns with the variables I'm saving
- Afterwards, click on the button to submit event, which triggers the addEvent() function to run

Here is the addEvent() function:

``` javascript
    async function addEvent() { 
        const year = document.getElementById('eventYear').value.trim();
        const description = document.getElementById('eventDescription').value.trim();
        if (!year || !description) {
            alert('Please fill in both the year and event description.');
            return;
        }
        const eventData = {
            year: parseInt(year, 10),
            description: description,
        };
        try {
            const response = await fetch(pythonURI + "/api/binary-history", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(eventData)
            });
        }
    }
    if (!response.ok) {
                throw new Error("Failed to add event");
            }
    alert("Event added successfully!");
    document.getElementById('eventYear').value = '';
    document.getElementById('eventDescription').value = '';
fetchAndDisplayBinaryHistory(); 
```

- The function gets the elements "year" and "description" through the input of the user, and raises an error if either of the elements are missing
- The data is saved into a dictionary where the year is parsed as an integer and the description is saves as a description
- The user inputted data is sent to my binary history api using the post method, and before it is sent it is converted from JSON into string format so it is readable by the API
- If the response is not 'ok' then it will tell the user that it failed to add the event, or else the event is added successfully and the eventYear and eventDescription textboxes are cleared

Here is the binary history api's GET and POST method:

``` python
class BinaryHistoryAPI:
    class _CRUD(Resource):
        def get(self):
            try:
                entries = BinaryHistory.query.all()
                results = [entry.read() for entry in entries]
                return jsonify(results)
            except Exception as e:
                return jsonify({"error": str(e)}), 500
        def post(self):
            data = request.get_json()
            post = BinaryHistory(data['year'], data['description'])
            post.create()
            return jsonify(post.read())
```

- Within the binary history API class is the CRUD method class that has the get and post self functions
    - The self varibale is used to gert access to the CRUD class itself so that the data requested by the user can be handled properly
- For the get method, python uses the query method from SQLAlchemy to retrieve the entries in the binary history table, and the list of entries are made into a list of dictionaries before being converted to JSON format so they can be interpreted by the frontend and changed into user-readale data
- The post method starts with obtaining the request data sent by the user (using the RESTful client API to retrieve the data) and turns the data into a new entry in the database
    - post.create() is used to make the post and return method is used to output the new entry in JSON format

As an output:
- A new entry (post) is created in the binary_history database, and in case of using postman, the new post is sent back to Postman and displayed in JSON format

#### List Requests:

``` javascript
const eventData = {
            year: parseInt(year, 10),
            description: description,
        };

        try {
            const response = await fetch(pythonURI + "/api/binary-history", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(eventData)
            });
        }
```

- The user inputted year and description are converted into a dictionary in JSON format, eventData, so that it can be sent to the backend through RESTful client API
- The eventData dictionary is converted to string before being sent to /api/binary-history through POST method

``` python
class _CRUD(Resource):
        def get(self):
            try:
                entries = BinaryHistory.query.all()
                results = [entry.read() for entry in entries]
                return jsonify(results)
```

- The database "BinaryHistory" is queried and returns a Python list of entries
    - The query method is from SQLAlchemy and retrieves the entries in the database
- The Python list undergoes "read" method from CRUD and is converted to JSON format so it becomes a dictionary

#### Algorithmic Code Requests

``` python
class _CRUD(Resource):
    def get(self):
        try:
            entries = BinaryHistory.query.all()
            results = [entry.read() for entry in entries]
            return jsonify(results)
        except Exception as e:
            return jsonify({"error": str(e)}), 500

    def post(self):
        data = request.get_json()
        post = BinaryHistory(data['year'], data['description'])
        post.create()
        return jsonify(post.read())

    def put(self):
        data = request.get_json()
        post = BinaryHistory.query.get(data['id'])
        post.year = data['year']
        post.description = data['description']
        post.update()
        return jsonify(post.read())

    def delete(self):
        data = request.get_json()
        post = BinaryHistory.query.get(data['id'])
        post.delete()
        return jsonify({"message": "Post deleted"})
```

- The API class with Resource as a parameter uses flask_restful.Resource to obtain the user-inputted data sent through RESTful client API in a string format
- The _CRUD class defined the HTTP methods for the API to handle data from the database and user, including get (reads a post), post (creates a new post), update (updates a post), and delete (deletes a post)
- All of the methods return a JSON formatted version of the result; for get it is reading all of the data in the table, for post and update it is reading the new post to the client, and for delete saying "Post deleted"
- Sequencing: For each of the method, the different lines of code go in sequential order
- Selection: For the get method, the output is a selection between raising an error or returning the response
- Iteration: For the get method, the "results" is a list of dictionaries, where it reads each entry retrieved from the database until there are no more entries left to read

#### Call to Algorithm Request:

``` javascript
async function fetchAndDisplayBinaryHistory() { 
        try {
            const response = await fetch(pythonURI + "/api/binary-history", {
                method: "GET",
                headers: {
                    "Content-Type": "application/json",
                }
            });
            if (!response.ok) {
                throw new Error("Network response failed");
            }
            const data = await response.json();
            data.sort((a, b) => a.year - b.year);
        }
}
```

- In the fetch function, the response is a fetch to the binary-history api endpoint in backend, using the GET method defined in the CRUD class
- A response from the fetch is waited for (await), and is the response is not ok the function seonds an error that the Network response failed
    - Having invalid data or using the wrong method causes this to happen, and thus the rest of the function is unable to run due to the data not being able to be handled properly
- Normally, the output (response) is converted into JSON format before being saved in a data variable, and the data is then manipulated to display certain results (as wanted) to the user on the site

## Personalized Project Reference:

#### Procedure

Capture and paste two program code segments you developed during the administration of this task that contain a student-developed procedure that implements an algorithm used in your program and a call to that procedure.

i. The first program code segment must be a student-developed procedure that:
Defines the procedure’s name and return type (if necessary)
Contains and uses one or more parameters that have an effect on the functionality of the procedure
Implements an algorithm that includes sequencing, selection, and iteration

``` javascript
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
```

ii. The second program code segment must show where your student-developed procedure is being called in your program.

``` javascript
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
```

#### List

Capture and paste two program code segments you developed during the administration of this task that contain a list (or other collection type) being used to manage complexity in your program.

i. The first program code segment must show how data have been stored in the list.

``` javascript
    const eventData = { // Create an object with the event data
        year: parseInt(year, 10), // Parse year as an integer
        description: description, // Add description
    };
```

ii. The second program code segment must show the data in the same list being used, such as creating new data from the existing data or accessing multiple elements in the list, as part of fulfilling the program’s purpose.

``` javascript
        fetch(pythonURI + "/api/binary-history", { // Send a POST request to add the event
            method: "POST", // Use POST method
            headers: {
                "Content-Type": "application/json", // Set request headers
            },
            body: JSON.stringify(eventData) // Send event data in the body of the request
        })
```

## Answers to FRQ Prompts:

Q: Identify an expected user of your program. Describe one way your program’s design meets the needs of this user. 

An expected user of this program is a student or researcher interested in the history of binary-related events and technological advancements. The program allows users to contribute historical events by entering a year and a description. The submitted events are then displayed in chronological order, making it easy for users to explore and learn about historical events related to binary and computing.

Q: Consider the first iteration statement included in the Procedure section of your Personalized Project Reference. Identify the number of times the body of your iteration statement will execute. Describe a condition or error that would cause your iteration statement to not terminate and cause an infinite loop. If no such condition or error exists, explain how the loop could be modified to cause an infinite loop.

The loop executes once for each event in the data array of my fetchAndDisplayBinaryHistory() function. If data contains 10 events, the loop runs 10 times. If it contains 100 events, the loop runs 100 times. Since forEach iterates over a finite list, it cannot cause an infinite loop. However, an infinite loop could occur if new elements were continuously added to data within the loop, such as:

``` javascript
data.forEach((event) => { 
    data.push({ year: 2000, description: "Looping forever!" }); // Adds new events inside the loop
});
```

Q: Consider the procedure included in part (i) of the Procedure section of your Personalized Project Reference. Describe a change to your procedure that will result in a run-time error. Explain why this change will result in a run-time error.

The addEvent function contains the following:

``` javascript
const year = document.getElementById('eventYear').value.trim();
const description = document.getElementById('eventDescription').value.trim();
```

If we modify the code to access a non-existent element:

``` javascript
const year = document.getElementById('wrongId').value.trim();
```

this would result in a TypeError because "document.getElementById('wrongId')" returns null, leading to an "Uncaught TypeError: Cannot read properties of null".

Q: Suppose you are provided with a procedure called isEqual (value1, value2). The procedure returns true if the two parameters value1 and value2 are equal in value and returns false otherwise. Using the list you identified in the List section of your Personalized Project Reference, explain in detailed steps an algorithm that uses isEqual to count the number of times a certain value appears in your list. Your explanation must be detailed enough for someone else to write the program code.

An example of such an algorithm is if we want to count how many times a particular year appears in the list. It would work as follows:
1. Initialize a counter to zero to keep track of how many times the target value appears.
2. Loop through each event in the data list.
3. Use isEqual to compare the event’s year with the target year.
4. If isEqual(event.year, targetYear) returns true, increase the counter by 1.
5. After the loop ends, return the counter.

<button><a href="{{site.baseurl}}/2025/03/04/tri2finalblog_IPYNB_2_.html">Go back to main blog</a></button>

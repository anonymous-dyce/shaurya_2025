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
            background: linear-gradient(135deg, #964b00, #ff8c00, #ffa756); /* 180deg for top-to-bottom gradient */
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
            color: black !important;
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
            background-color: lightgray !important; /* Light gray on hover */
            transform: scale(1.05);
        }
        .regularButton:active {
            background-color: grey !important; /* Slightly darker gray when clicked */
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
<p>NOTE: The function won't work because the addEvent() function is not included as onclick in the button</p>
<button class="regularButton"><a href="{{site.baseurl}}/binary_history/blog">Check out my Blog!</a></button>
<script>
    // NOTE: THIS CODE IS NOT THE ACTUAL CODE I USED TO CONNECT TO API, IT WILL NOT SAVE ANY ENTERED DATA
        // Default events data
        const defaultEvents = [
            { description: "Gottfried Wilhelm Leibniz conceives the idea of the binary numeral system in his essay 'Explication de l'Arithmétique Binaire'.", year: "1679" },
            { description: "Leibniz formally publishes his work on the binary numeral system in 'Explication de l'Arithmétique Binaire'.", year: "1703" },
            { description: "George Boole develops Boolean algebra, which becomes foundational for binary logic.", year: "1847" },
            { description: "George Boole publishes 'An Investigation of the Laws of Thought', further detailing Boolean algebra.", year: "1854" },
            { description: "Claude Shannon applies Boolean algebra to design electronic circuits in his master's thesis.", year: "1937" },
            { description: "John Atanasoff and Clifford Berry create the Atanasoff-Berry Computer (ABC), which uses binary.", year: "1939" },
            { description: "John von Neumann outlines the architecture of modern computers, emphasizing binary.", year: "1945" },
            { description: "The ENIAC computer is completed, though it uses decimal rather than binary.", year: "1946" },
            { description: "Claude Shannon publishes 'A Mathematical Theory of Communication', linking binary to information theory.", year: "1948" },
            { description: "Alan Turing's work on binary-based computation contributes to the development of modern computer science.", year: "1950" },
            { description: "The UNIVAC I, the first commercial computer, uses binary in its operations.", year: "1951" },
            { description: "Binary-coded decimal (BCD) becomes widely adopted for numerical representation in computing.", year: "1960" },
            { description: "ASCII (American Standard Code for Information Interchange) is introduced, using binary to represent characters.", year: "1964" },
            { description: "The UNIX operating system is created, relying heavily on binary representations.", year: "1969" },
            { description: "Intel releases the 4004 microprocessor, the first commercially available processor based on binary.", year: "1971" },
            { description: "IBM introduces the PC, making binary-based computing accessible to the public.", year: "1980" },
            { description: "The World Wide Web is introduced, built upon binary protocols and systems.", year: "1991" },
            { description: "The Y2K problem highlights the importance of binary in year representation and storage.", year: "2000" },
            { description: "Bitcoin, based on binary and cryptographic principles, is introduced.", year: "2008" }
        ];
        // Function to display binary history from default events
        function fetchAndDisplayBinaryHistory() {
            const data = defaultEvents;
            data.sort((a, b) => a.year - b.year);
            const historyContainer = document.getElementById('binary-history');
            historyContainer.innerHTML = '';
            data.forEach((event) => {
                const eventDiv = document.createElement('div');
                eventDiv.classList.add('event');
                const title = document.createElement('h3');
                title.textContent = event.year;
                const description = document.createElement('p');
                description.textContent = event.description;
                eventDiv.appendChild(title);
                eventDiv.appendChild(description);
                historyContainer.appendChild(eventDiv);
            });
        }
        // Function to add a new event
        function addEvent() {
            const year = document.getElementById('eventYear').value.trim();
            const description = document.getElementById('eventDescription').value.trim();
            if (!year || !description) {
                alert('Please fill in both the year and event description.');
                return;
            }
            const eventDiv = document.createElement('div');
            eventDiv.classList.add('event');
            const title = document.createElement('h3');
            title.textContent = year;
            const descriptionElement = document.createElement('p');
            descriptionElement.textContent = description;
            eventDiv.appendChild(title);
            eventDiv.appendChild(descriptionElement);
            const historyContainer = document.getElementById('binary-history');
            historyContainer.appendChild(eventDiv);
            document.getElementById('eventYear').value = '';
            document.getElementById('eventDescription').value = '';
        }
        // Initial fetch to display default history
        fetchAndDisplayBinaryHistory();
    </script>
</body>
</html>
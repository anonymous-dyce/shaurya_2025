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
<button class="regularButton" >Submit Event</button>
<p>NOTE: The function won't work because the addEvent() function is not included as onclick in the button</p>
<button class="regularButton"><a href="{{site.baseurl}}/binary_history/blog">Check out my Blog!</a></button>

</body>
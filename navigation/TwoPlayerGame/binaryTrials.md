---
layout: page
title: Binary Trials 
search_exclude: true
permalink: /trials/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Trials</title>
    <style>
        body {
            background: linear-gradient(150deg,rgb(72, 14, 14),rgb(148, 36, 36),rgb(160, 20, 20),rgb(123, 15, 15));
            color: #ffffff;
            font-family: Arial, sans-serif;
            text-align: center;
            overflow-y: auto;
        }
        p {
            color: black;
            font-size: 18px;
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
    <h3>Welcome to Binary Trials! Make sure you have someone to play with!</h3>
    <p>Partner - The history of binary, where both people have to work together and answer questions to win!</p>
    <p></p>
    <button class="regularButton"><a href="{{site.baseurl}}/trialsPartners">Partner Game</a></button>
</body>
</html>
---
layout: base
title: Shaurya's Site
description: Home Page
hide: true
---

My name is Shaurya and I am in 11th grade.

<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background: black;
      color: #ffffff;
      font-family: Arial, sans-serif;
    }
    .button {
      background-color: #ff4d4d !important;
      color: #ffffff !important;
      text-decoration: none;
      font-weight: bold;
      font-family: Arial, sans-serif;
      display: inline-block;
      padding: 15px 20px;
      border-radius: 20px;
      transition: transform 0.2s ease, background-color 0.2s ease;
      text-align: center;
      margin-top: 10px; /* Adds space above the button */
    }
    .button:hover {
      transform: scale(1.05);
      background-color: #e60000 !important;
    }
    .button:active {
      transform: scale(0.95);
      background-color: #b30000 !important;
    }
    /* Add margin above paragraphs */
    p {
      margin-top: 40px; /* Adds space above paragraphs */
    }
    .dropdown {
      position: relative;
      display: inline-block;
      margin-bottom: 140px;
    }
    .dropdown button {
      background-color: #ff4d4d !important;
      color: white;
      text-decoration: none;
      font-weight: bold;
      font-family: Arial, sans-serif;
      display: inline-block;
      padding: 15px 20px;
      border-radius: 5px;
      transition: transform 0.2s ease, background-color 0.2s ease;
      text-align: center;
      margin-top: 20px; /* Adds space above the dropdown button */
    }
    .dropdown button:hover {
      transform: scale(1.05);
      background-color: #e60000 !important;
    }
    .dropdown button:active {
      transform: scale(0.95);
      background-color: #e60000 !important;
    }
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: blue !important;
      color: white !important;
      min-width: 350px;
      box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
      border-radius: 5px;
      z-index: 1;
      opacity: 0;
      transform: translateY(10px);
      transition: transform 0.2s ease, background-color 0.2s ease, color;
    }
    .dropdown-content a {
      color: white !important;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      border-radius: 5px;
      transition: transform 0.2s ease, background-color 0.2s ease, color;
    }
    .dropdown-content a:hover {
      transform: scale(1.05);
      background-color: turquoise !important;
      color: black !important
    }
    .dropdown:hover .dropdown-content {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>

<body>
  <div class="dropdown">
    <button class="dropbtn" onclick="toggleDropdown()">Directory</button>
    <div class="dropdown-content" id="myDropdown">
      <a href="http://127.0.0.1:4100/shaurya_2025/studentCars/">Student Cars (Sprint 3)</a>
      <a href="http://127.0.0.1:4100/shaurya_2025/binary_history">The History of Binary... (Sprint 4 & 5)</a>
      <a href="http://127.0.0.1:4100/shaurya_2025/blogs/">Blogs</a>
    </div>
  </div>

  <p>This is a song by one of my favorite Hindi Rappers named Badshah, where he features an American Rapper (Lil Baby) and a Spanish Rapper (J Balvin). CAUTION: Explicit lyrics by Lil Baby & single F-word in the very beginning.</p>

  <button class="button" onclick="window.location.href='https://www.youtube.com/watch?v=sPn2HP8cAbo'">Voodoo (Lil Baby Remix)</button>

  <p>This is a list of Bollywood songs, as well as some personal favorite Hindi songs; Bollywood songs incorporate both modernized and cultural Indian music, and they are my favorite category of songs:</p>

  <button class="button" onclick="window.location.href='https://open.spotify.com/playlist/55cg4nkj03sCr4SgkP57D9'">Fav Bollywood Songs</button>

  <p>This is a button that helps you finally be done with programming in this class:</p>
  
  <button class="button">THE ULTIMATE ESCAPE FROM CSP</button>

  <p>(P.S. it doesn't lead anywhere because you are never 'done' with programming in this class, you always have something to code!)</p>

</body>
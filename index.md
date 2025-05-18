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
      margin-bottom: 40px
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
      background-color: #e60000 !important;
    }
    .dropdown button:active {
      background-color: #e60000 !important;
    }
    .dropdown-content a {
      display: block;
      padding: 12px 16px;
      color: white !important;
      text-decoration: none;
      font-family: Arial, sans-serif;
      font-weight: bold;
      transition: background 0.2s;
    }
    .dropdown-content a:hover {
      background: #003366 !important;
    }
    .dropdown-content {
      display: block;
      max-height: 0;
      overflow: hidden;
      opacity: 0;
      background-color: blue !important;
      color: white !important;
      min-width: 350px;
      box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
      border-radius: 5px;
      transition: max-height 0.3s cubic-bezier(.4,0,.2,1), opacity 0.3s cubic-bezier(.4,0,.2,1);
      margin-bottom: 0;
    }
    .dropdown.open .dropdown-content {
      max-height: 400px; /* Adjust based on menu size */
      opacity: 1;
      margin-bottom: 20px; /* Space between menu and content */
    }
    .shifted-down {
      transition: margin-top 0.3s cubic-bezier(.4,0,.2,1);
      margin-top: 0;
    }
    .dropdown.open ~ #mainContent.shifted-down {
      margin-top: 0; /* No extra margin needed since menu takes up space */
    }
  </style>
</head>

<body>
  <div class="dropdown" id="dropdownMenu">
    <button class="dropbtn" onclick="toggleDropdown()">Directory</button>
    <div class="dropdown-content" id="myDropdown">
      <a href="{{site.baseurl}}/studentCars/">Student Cars (Sprint 3)</a>
      <a href="{{site.baseurl}}/binary_history">The History of Binary... (Sprint 4 & 5)</a>
      <a href="{{site.baseurl}}/trials/">Binary Trials - Partners Game (Sprint 6)</a>
      <a href="{{site.baseurl}}/labsim2.0/">PilotCity - BioSKANZ - Trivia Game (Sprint 7)</a>
      <a href="{{site.baseurl}}/blogs/">Blogs</a>
    </div>
  </div>

  <div id="mainContent">
    <p>This is a song by one of my favorite Hindi Rappers named Badshah, where he features an American Rapper (Lil Baby) and a Spanish Rapper (J Balvin). CAUTION: Explicit lyrics.</p>
    <button class="button" onclick="window.location.href='https://www.youtube.com/watch?v=sPn2HP8cAbo'">Voodoo (Lil Baby Remix)</button>
    <p>This is a list of Bollywood songs, as well as some personal favorite Hindi songs; Bollywood songs incorporate both modernized and cultural Indian music, and they are my favorite category of songs.</p>
    <button class="button" onclick="window.location.href='https://open.spotify.com/playlist/55cg4nkj03sCr4SgkP57D9'">Fav Bollywood Songs</button>
    <p>This is a button that helps you finally be done with programming in this class:</p>
    <button class="button">THE ULTIMATE ESCAPE FROM CSP</button>
    <p>(P.S. it doesn't lead anywhere because you are never 'done' with programming in this class, you always have something to code!)</p>
  </div>
</body>

<script>
  const dropdown = document.getElementById('dropdownMenu');
  const mainContent = document.getElementById('mainContent');

  dropdown.addEventListener('mouseenter', () => {
    dropdown.classList.add('open');
    mainContent.classList.add('shifted-down');
  });
  dropdown.addEventListener('mouseleave', () => {
    dropdown.classList.remove('open');
    mainContent.classList.remove('shifted-down');
  });
</script>
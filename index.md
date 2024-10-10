---
layout: base
title: Shaurya's Site
description: Home Page
hide: true
---

My name is Shaurya and I am in 11th grade.

<html lang="en">

<body>
    <div class="dropdown">
        <button class="dropbtn" onclick="toggleDropdown()">Directory</button>
        <div class="dropdown-content" id="myDropdown">
            <a href="http://127.0.0.1:4100/shaurya_2025/about/">About</a>
            <a href="http://127.0.0.1:4100/shaurya_2025/README4YML.html">Readme</a>
            <a href="http://127.0.0.1:4100/shaurya_2025/blogs/">Blogs</a>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      transition: background-color 1s ease; /* Smooth transition for background color */
    }
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(255, 255, 255, 0.8); /* White overlay */
      display: none; /* Hide overlay initially */
      z-index: 9998; /* Behind the loader */
      transition: opacity 1s ease; /* Smooth transition for the overlay */
    }
    .loader {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 9999;
      display: none; /* Hide loader initially */
    }
    .dots {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 8px;
    }
    .dot {
      width: 20px; /* Size of the dots */
      height: 20px;
      border-radius: 50%;
      background-color: #4CAF50; /* Dot color */
      animation: bounce 0.6s infinite alternate; /* Bounce animation */
    }
    .dot:nth-child(1) { animation-delay: 0s; }
    .dot:nth-child(2) { animation-delay: 0.2s; }
    .dot:nth-child(3) { animation-delay: 0.4s; }
    @keyframes bounce {
      0% { transform: translateY(0); }
      100% { transform: translateY(-15px); }
    }
    .button-custom {
      background-color: #2b669a; /* Main theme color */
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }
    .button-custom:hover {
      background-color: #1d4f73; /* Darker shade for hover */
      transform: scale(1.05); /* Slightly enlarges button on hover */
    }
    .button-custom:active {
      background-color: #163d59; /* Even darker on click */
      transform: scale(0.98); /* Shrinks button slightly on click */
    }
    .button-custom:focus {
      outline: none;
      box-shadow: 0 0 5px #2b669a; /* Adds a shadow on focus */
    }
    .dropdown {
      position: relative;
      display: inline-block;
    }
    .dropdown button {
      background-color: #3498db;
      color: white;
      padding: 14px 20px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .dropdown button:hover {
      background-color: #2980b9;
    }
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #34495e;
      min-width: 160px;
      box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
      border-radius: 8px;
      z-index: 1;
      opacity: 0;
      transform: translateY(10px);
      transition: opacity 0.3s ease, transform 0.3s ease;
    }
    .dropdown-content a {
      color: white;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      border-radius: 8px;
      transition: background-color 0.3s ease;
    }
    .dropdown-content a:hover {
      background-color: #1abc9c;
    }
    .dropdown:hover .dropdown-content {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
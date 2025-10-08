---
layout: page
title: Reflection on Student 2026 Project
toc: True
permalink: /blogs/student_2026_blog/
categories: ["Shaurya's Blogs"]
---

When I joined the Open Coding Society, I set out to solve a real problem: many educators want to teach CS, but they often lack the tools, confidence, or technical background to get started. I wanted to change that by building something simple, engaging, and empowering.

That’s how Student 2026 was born — a full-stack, web-based learning platform that helps teachers learn foundational computing concepts through interactive lessons, quizzes, and a competitive leaderboard.

#### What I Built

As a developer, I designed and developed features in Student 2026, from frontend interactivity to backend score tracking. Here's a breakdown of what I accomplished:

Interactive Lessons

- Wrote and designed modular lesson pages for 3 CS topics: workflow, accounts, and page structure.

- Used JavaScript DOM manipulation to control navigation between lessons, ensuring a smooth UX.

- Created a persistent points system using localStorage to track student progress.

Quizzes w/ Progress Tracking

- Built custom quiz modules for each lesson, complete with multiple-choice logic, auto-grading & feedback,and a save/reset point system to encourage retries

Connected quiz results to a scoring system that calculates combined progress.

Leaderboard API

- Designed a RESTful API in Flask to store and retrieve scores.

- Used JWT authentication to restrict score submissions to logged-in users only.

- Built an intuitive UI to show top scorers, encouraging engagement and competition.

Dev Tools & Version Control

- Structured the project using modular JS, organized CSS, and version control with GitHub.

- Managed configuration using environment-based fetch URIs and standardized config.js files for API routing.

Documentation & Blogging

- Wrote a Help Me file in Markdown for students and teachers to understand how the app works.

- Covered features like score saving, quiz resetting, and how to interpret the leaderboard.

- Wrote retrospectives and technical blogs on how I implemented features like the leaderboard API and quiz logic.

#### What I Learned

Technical Growth:

- Built real-world experience with REST APIs, user authentication, and state management.

- Learned to debug async data flow between frontend and backend (especially around localStorage, fetch(), and JWTs).

- Strengthened my full-stack dev skills by architecting both frontend and backend logic from scratch.

Personal Growth:

- Discovered how rewarding it is to build for real users.

- Learned how to communicate technical systems to non-technical users through documentation and walkthroughs.

#### Growth moment:

While I did accomplish several things, I also encountered challenges what allowed me to grow. For instance, I initially had a quiz in a test format, which was extremely monotonous and would make the user uninterested in the site. However, my teacher told me to make it more engaging, which allowed me to research into more creative ways of learning. From there, I decided to make flashcards that tracked your progress, and a point system that allowed you to see your performance.

While we ended up not implementing the flashcards and point system, this experience allowed me to go deeper into my frontend code, while improving skills such as adaptability and collaboration.

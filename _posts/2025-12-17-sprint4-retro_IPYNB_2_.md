---
layout: page
title: Retrospective on CSA Sprint 4
toc: True
permalink: /blogs/sprint4retrospective/
categories: ["Shaurya's Blogs"]
---

## Reflection Timeline:

At the beginning of the trimester, I worked on planning for the upcoming sprint. I helped in breaking down our overall goals and to do list into smaller phases that we could divide up, such as data persistence, theming engine, and theming applications. I listed detailed things we needed to work on for our final product so that we could go from a broad idea presented to us to work on to tangible activities that could be completed (or broken down more into smaller tasks).

Then, I got to work on user preferences. I wanted to help implement user preferences within the Infograph for Tools and Equipment, and that made me realize a bigger issue. The infograph was part of the tailwind css we were using, and tailwind itself was completely disconnected from the dashboard. This was also causing pages like onboarding adventure to incorrectly display preferences. Because of this, I got to work on implementing the preferences within files such as dashboard and infograph, as well as several individual markdown files. I was able to stop bugs from occuring with the home page's text, and even got preferences to show up in the places that were stuck on default styling.

Afterwards (and most recently), I worked on the calculator lesson. My job was to write the lesson for the calculator that would be presented for CSSE onboarding. Although we had conflicts and misunderstandings about the lesson content, I ended up creating the lesson structure with different sections of teaching code, as well as notes and homework hacks.

### Highlighting Sprint 4:

Here is a table of the skills I gained:

| **Skill** | **Description** | **Future Focus** |
|------------|-----------------|------------------|
| Gemini API Integration | Learned to connect Gemini API to backend systems for AI-powered suggestions on user stlying. | Allow user to automatically implement Gemini's styling recommendations rather than making changes themselves. |
| Dynamic styling | Worked on implementing user preferences on the site, such as text color, background color, and font family, and fixed styling issues on the home page and dashboard. | Deepen understanding of html/css in dashbord and create new preferences. |
| Tailwind CSS Connectivity | Worked on connecting user preferences styling to Tailwind CSS and infographs, allowing for styling to show up on infographs (eg. tools and equipment) and onboarding pages. | Ensure preferences are smoothly implemented throughout the site and simplify CSS to solely use preferences. |
| Spring Boot Framework | Built RESTful API endpoint using Spring Boot to handle routes and support full-stack app functionality. | Get spring to connect with frontend for user preferences recommendations and potentially create lessons on how to fix different types of backend errors. |
| Frontend–Backend Integration | Connected web frontends to Spring Boot backend, managing data flow. | Explore modern frontend frameworks like React for real-time updates and API communication. |
| Helping CSSE/CSP | Created lessons to help CSSE students code their own calculator as part of onboarding adventure. Integrated Gemini into JavaScript lessons for CSP for real-time feedback. | Make lessons for math, such as Trigonometry and Precalculus (I am currently figuring out which problems and topics will be most efficient to teach). |

### Feature:

While Trimester 2 was going on, I took out time throughout each week to work on my best feature, integrating the Gemini API into the profile preferences to enable user personalization. Users interact with a dedicated "Ask AI" interface, providing natural language descriptions—such as aesthetic moods ("modern," "playful"), specific color theory terms (tints, hues), and thematic concepts—to articulate their ideal site theme. This moves customization beyond static menus, allowing students to instantly generate themes tailored to their creative vision.

The user's prompt is transmitted from the frontend to the Spring backend. The backend then constructs a detailed prompt, including the user's input alongsideconstraints (like the approved list of seven font families: Inter, Roboto, etc.), and directs Gemini to act as a UI/UX design assistant.

Gemini's output includes the recommended hex codes for key elements (background, buttons, text, selection highlights) and the ideal font family. This generated theme configuration is returned to the frontend's "Response Box," allowing the user to review, confirm, and apply a sophisticated, algorithmically-generated theme based purely on their textual preferences.

### Future:

In the next sprint, I would like to implement the Java that I have learned and get to use springboot, rather than simply working on frontend features. This will help me expand on my programming knowledge and better prepare for the AP Exam. 

I want to also ensure spring doesn't crash due to issues with the database, and that the frontend-to-backend connection doesn't face any issues, such as CORS. I felt like these two were the biggest issues I faced when connecting pages to spring, and do not want to constantly face these issues. I could make a troubleshooting blog for how to tackle several types of issues (in spring and APIs), so that other people don't face similar (or other) issues as well.

## Analytics Review:

Overall, I feel my contributions have been better these past two weeks as I have been coding and writing lessons. I am actually committing a lot more of my changes rather than committing lots of files at once, and my commit history is looking decent. Because of the holidays and working more on planning rather than coding, my commits are a lot less in November.

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

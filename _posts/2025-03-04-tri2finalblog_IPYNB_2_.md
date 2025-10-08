---
layout: page
title: Tri 2 Final Exam Blog
search_exclude: True
toc: True
permalink: /blogs/t2finalblog
categories: ["Shaurya's Blogs"]
---

## 5 things I did over 12 weeks in Trimester 2

1. Binary Quiz Grading Backend
    - I initially worked on the model and API for a binary quiz
    - I created a model that had sections for quiz attempt number and score
    - I worked with Rutvik, who saved quiz questions, and Shriya, who worked on frontend
    - Shriya took over binary quiz as her feature but my database helped her create her own

2. Binary History Full Stack Feature
    - My full stack feature displays binary history events and allows users to add events to the list
    - My database saves event year and description and connects to frontend using API endpoint
    - For frontend, I worked on fetching the events from backend using GET method and displaying them from oldest to most recent
    - For interactivity, I created an input at the bottom of the page where users can add their own event to show up in the database

3. Binary Trials
    - Me and rutvik partnered up to work on a series of games called binary trials 
        - I had to work on the game where two players had to work as a team to win
    - In the game, 2 players take turns answering questions about binary history and have to stay away from each other
    - If they touch the game ends, so they must stay away from each other as long as possible
    - Due to my game, my full stack feature is now a "study guide" for players to memorize the events and add their own to the game

4. Collaboration
    - This trimester, our team had a rough start and was disorganized in terms of working as group
    - Later, we began to have standup meetings and used Slack and iMessages to communicate about progress and issues
    - We also helped each other with understanding topics: for instance, I helped my teammate understand parts of Big Idea 4
<img src="{{ site.baseurl }}/images/t2feb_img1.png" alt="Binary History">
    - Overall, our collaboration improved significantly, and by the end of this tri we have an organized binary page with each of our games matching an overall theme and a functioning backend UI
5. Frontend UX Engineer
    - As the Frontend UX Engineer of our group, I helped manage the styling of our overall site and ensure consistency throuhgout the features
    - I helped by styling the home page and organizing links that led to other pages so that our home page was organized
<img src="{{ site.baseurl }}/images/t2feb_img2.png" alt="Binary History">
    - Additionally, I ensured evreryone's feature had the same styling structure, such as background, text, buttons, textboxes, etc.
    - For our binary trials series, I created the trials directory which had a styling consistent to the two features, could be directly accessed by the home page, and had links to our features
<img src="{{ site.baseurl }}/images/t2feb_img3.png" alt="Binary History">

## N@TM Experience

<img src="{{ site.baseurl }}/images/t2feb_img4.jpg" alt="Binary History">

Overall, N@TM was an amazing experience, as I got to present my individual feature to several students and parents, and I was able to take notice of other people's features, including those from CSP, CSA, and CSSE. I took interest in one of the people's features at the event, Darsh, and I interviewed him about the different parts of his group and individual feature. Additionally, I ran into my friend Nikhil N and he needed help with preparing for the CSP final, so I recorded my conversation with him and helped him prepare for the final.

<button onclick="window.location.href='https://www.youtube.com/watch?v=Z7EaVYv4gLE'">Here is a link to my interview and conversation</button>

## Project Feature Write-Up:

<button><a href="{{site.baseurl}}/2025/03/04/t2fbwriteup_IPYNB_2_.html">Here is a link to my write-up in CPT/FRQ terms</a></button>

## MCQ:

<button><a href="{{site.baseurl}}/2025/03/10/t2finalmc_tc_IPYNB_2_.html">This is my test corrections for the questions I rushed on my MCQ</a></button>

## Retrospective

- Overall, this trimester signifantly improved me not just as a coder, but as a member of a team
    - My strengths for this trimester were: 
        - Consistency, as I made sure to meet all requirements before each live review during the tri
        - Collaboration, as I collaborated with my teammates so we all had similar styling and UI throughout our site, and I regularly helped people with the frontend of their feature
        - Understanding of code: even though I had never coded in Javascript or Advanced Python / SQLite before, I tried my best to understand each line of code in my model, API, and frontend, and I understood how functions such as fetching, posting, schema, etc. worked
    - My weaknesses for this trimester were:
        - Time management; I would often work on my code and live review requirements during office hours or lunch rather than doing it as homework, because I frequently procrastinated my CSP work at home
        - Getting distracted; my teammates would come to me for help frequently and talk about non-CSP related topics frequently, and a lot of the time I would become involved in their conversation and helping them rather than working on my code

- In the future, I wish to get an internship for computer science where I can work on full stack projects and use my CSP knowledge, as well as individual learning, to become a successful intern.
- I also want to pursue Electrical Engineering and Computer Science as my majors, so that I can combine both my softwarw and hardware skills to work on projects for tech companies.

#### Reflection on project by creating next steps plans for strengths and weaknesses

Next steps for strengths:
- Continue on team collaboration and communication by making the group a safe place to ask questions and promote conversation
- Maintain my understanding of the code by spending time after school reviewing the code and connecting the dots of where everything goes even as the code gets harder and harder
Next steps for weaknesses:
- Time Management: Break whatever I was trying to finish for the day into smaller chunks and take short breaks inbetween so I don’t burn myself out and waste a long time on a break
- Not understanding CPT requirements properly: To overcome this I will watch the collegeboard videos in more depth and take notes to really understand what is needed from me
- Distractions: Stay focused and on task by looking at the overall picture of what is happening and not getting worried about the small details.

#### Reflection on individual strengths/weaknesses regarding code.

Strengths:
- Complete Full-Stack Integration
- Combining frontend (JavaScript, HTML), backend (Flask, Python), and database (SQLAlchemy)
- Users can Create and Read events in binary history
- Utilizing Fetch API in add event and display binary history functions for real-time updates

Seamless JSON to DOM Handling
- Retrieves history events from the backend in JSON format
- Dynamically modifies the DOM to reflect updated list of events

Database Management & Restore
- Stores history event data persistently using SQLAlchemy
- Includes a restore function to reset or backup data

Weaknesses:
- My page looks very bland with only the list of history events, I could have made the page more interactive
- My feature is lacking an update and delete function; I initially had one but because it constantly ran into errors, I had to remove it

#### Next Steps
I would like for users to be able to look at the previous ages that they had inputted and be able to compare their efficiency in achieving their goal. A visual representation of this would be most effective such as a bar graph or a line graph to show the rate at which they are achieving their goal. To achieve the chart, a function would have to be created so that only integers could be inputted for their age and a function to create and display a graph would have to be created. A spellchecker is something that I believe could enhance the UI of my feature, making the UI more appealing to users and just overall providing a better experience.
Things I struggled with over the course of this trimester

#### Extra: A memorable part of this tri
One memorable thing in terms of code over the course of this trimester was getting my API PUT function to work properly. I was constantly getting 500 Internal Server errors. I also struggled a lot to fix the restore function. Every time I would run the restore function, lots of errors would show up. To fix this I did a deep dive into the scripts restore file where I learned that one of the models in the database had a few errors causing the error in restore. I was then able to fix those errors and resolve the issue.
To solve these problems I would use debugging methods such as print statements to see where the code was going, and breakpoints to truly understand what the code was doing.

## Self Grade:

5 things for DOCSE: 4.8/5
- I would give myself this score because even though I worked on multiple projects and stuck to my individual feature a few weeks after the tri started, I was able to gain a lot more experience by working on several features; by working on the backend for quiz grading and my binary history, I now feel more experienced with creating a database schema and making an API endpoint.

Full stack project demo: 1.8/2
- Overall, I feel like my full stack feature meets most of the CPT requirements and is very user interactive, expecially the game I worked on that has become a part of my feature. Also, I was able to present really well at N@TM and got overall positive feedback from the audience. However, I can spend more time trying to understand CPT requirements and how I can develop my project to more specifically align with CPT/PPR.

Project Feature Write-up: 1/1
- In my write up I talked about how the different parts of my project align with CPT requirements, such as Input/Output, Algorithmic Code Requests, List Requests, and a Call to Algorithm. I also taked about how my project fulfills my response for the PPR, and how I will answer the FRQs for my feature.

MCQ: 0.85/1
- I completed the MCQ, but I had to rush through a lot of the questions as I had done the exam right before presenting what I would do for my live review (which was 24 hours prior to the day of the final). However, I completed most of my test corrections for it, and I spent time understanding the questions I rushed through.

10th Point: 1/1
- I feel like I earned the 10th point because I had a throrough interview redarding Darsh's project and with Nikhil needing help for his final prep. I also talked about my strengths and weaknesses both regarding my code and individual skills, as well as my plans for the future regarding computer science and one memorable thing from this trimester.

Overall score: 9.35/10
- I feel like I made significant improvements throughout this trimester, and because of my ability to consistently deliver good quality code and output, as well as thoroughly explaining connections and applications of my work to collegeboard and class requirements, I believe I deserve this score. During next trimester, I hope to continue to make improvements and strive for success as we go through topics in the Data Structures Course.



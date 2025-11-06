---
layout: page
title: Retrospective on Trimester 1
toc: True
permalink: /blogs/tri1retrospective/
categories: ["Shaurya's Blogs"]
---

## AP CSA Practice Exam:

Here is my performance in each section of the exam:

| Unit                     | Questions Correct (out of total) | Percentage |
|---------------------------|----------------------------------|-------------|
| Using Objects and Methods | 9 out of 12                     | 75%         |
| Selection and Iteration   | 9 out of 13                     | 69%         |
| Class Creation            | 6 out of 7                      | 86%         |
| Data Collections          | 12 out of 16                    | 75%         |
| **Total**                 | **31 out of 42**                | **74%**     |


The topics that I did not do well on were: 1.15 (String Manipulation), 2.4 (Nested if Statements), 2.8 (for loops), and 4.8 (ArrayList Methods). I need to work on these topics more thoroughly and improve in order to perform better on future MCQs and the AP Exam.

However, the topics that I performed well on were 1.14 (Calling Instance Methods), 3.2 (Impact of Program Design), 3.5 (Methods: How to Write Them), and 4.3 (Array Creation and Access). These are areas of less concern, and I only need to review and do some practice on these topics.

I reflected on my performance using the graphs and tables below. These will also help me prepare for future MC exams.

#### What did I learn?

- Taking this quiz helped me understand the structure of AP CSA exam questions and key topics such as using objects and methods, selection and iteration, and data collections through Java syntax. These questions seem interesting to me and I will make sure to go over the topics, especially of the questions I missed, so that I can do better on future practice exams.

- Because I had learned about the fundamentals of programming and syntax, I was easily able to understand more than half of the questions, such as the ones for class creation, using methods and objects, and even some within data collections. 

- I find Java syntax and functionality to have many similarities to Python, which is why I could use my Python knowledge for many questions where we had to understand code.

#### Here is my overall performance on the 11 questions I got wrong, separated by each big idea:

<img src="{{ site.baseurl }}/images/csa_prex_mc.png">

Although I had the same number of questions wrong for BI 2 and 4, I understood more of the questions in BI 2 than BI 4. BI 3 had roughly the same amount of questions not understood as BI 2, and each BI had one question where I did not understand the question or the concept.

[Here is the link to my corrections and approach for each missed problem](https://github.com/anonymous-dyce/shaurya_2025/issues/12)

## Reflection Timeline:

At the beginning of the year, I came in with only my rusty CSP knowledge. I had not done any programming as I had gone to India over the summer, and I had to re-look at the code on my recent full-stack project, BioSKANZ. I did not know anything about Java whatsoever and was only content with the Python, SQLite, JavaScript, HTML, and API knowledge I already had.

During the Tools sprint, I, Arnav, and Ahaan worked on creating new lessons on the open coding society site. I wanted to gain further experience from this sprint, so I worked on integrating Gemini into FRQ questions and having the questions serve as checkpoints between each lesson. I later moved the Gemini prompt/response system, including my API Key, to the spring backend to ensure protection of my key (continued in "cool feature" section). 

During the Java fundamentals (CSA lessons) sprint, I made sure to do all popcorn and homework hacks, including some of the extra credit, as this will help me with my Java knowledge for the rest of the year. Also, it will greatly help me on my AP Exam; as I have already seen, it helped me with many of the questions on the Practice Exam.

During the Frontend Quest sprint, I worked on submodule 1 (the overview of frontend). I created a module that was interactive (through FRQ and MC questions, as well as a Synergy Demo), appealing (through colorful styling, headers, and bullet points rather than paragraphs), and easy to understand (covered content at a CSSE/beginner-level CSP comprehension).

### Highlighting Sprint 1 (includes the cool feature I worked on):

Here is a table of the skills I gained:

| **Skill** | **Description** | **Future Focus** |
|------------|-----------------|------------------|
| Gemini API Integration | Learned to connect Gemini API to backend systems for AI-powered responses, enabling smart feedback. | Integrate Gemini features into more personalized learning platforms. |
| Java Programming | Gained experience coding in Java to develop backend logic and handle user data. | Deepen understanding of data structures and backend optimization techniques. |
| Java Tools (JDK, JBang) | Used JDK for compiling and running Java applications and explored JBang for Jupyter Notebooks. | Leverage JBang for prototyping of backend utilities. |
| Spring Boot Framework | Built RESTful API endpoint using Spring Boot to handle routes and support full-stack app functionality. | Learn more about how the spring repository works, including maven, Main.java, and databases. |
| Frontend–Backend Integration | Connected web frontends to Spring Boot backend, managing data flow. | Explore modern frontend frameworks like React for real-time updates and API communication. |

Overall, I got Gemini to work making a fetch request to backend (by sending the FRQ question and student response as instances in a data class), processing the data through a Gemini controller file in the backend, receiving a response from Gemini after entering the data as part of a prompt, sending Gemini's response to frontend as an instance within the same data class, and processing Gemini's response to appear in frontend. I will integrate Gemini whenever I get the chance for future sprints and help the current team assigned for Gemini.

### N@TM Reflection:

Night at The Museum was very fun. I arrived there on time to be able to look at the projects being presented by CSSE and CSP. CSSE projects made me realize how versatile javascript and frontend development really is, and I would definitely recommend it to a friend who is new to programming. CSP made me remember about the time I got started with programming and how I had to overcome challenges in tools setup while working on frontend sprints in Trimester 1.

As a member of CSA, I felt it was my rightful duty to give comments to the CSP/CSSE people that presented to me, and I made sure to leave comments that they could understand for the programming level they are at. When I presented, it was mainly other parents that looked at our presentation and gave us feedback. The feedback we got will help us improve for future sprints. Overall, I was able to give and take a lot of information through this memorable event.

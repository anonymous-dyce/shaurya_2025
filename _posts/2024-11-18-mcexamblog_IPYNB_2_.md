---
layout: page
title: Reflection on Sprint 3 and 2018 Practice MCQ
toc: True
permalink: /blogs/2018mcq-sprint3/
categories: ["Shaurya's Blogs"]
---

### Sprint 3 Accomplishments

For the last 3-4 weeks of Trimester 1, me and my group made Nighthawk Cars, which was a branch of our period's social media pages called "Vote for the GOAT". Nighthawk Cars is a series of pages about different types of cars; each page contains a different category of car and has examples of cars in that category, the average price of cars, the most and least expensive car's price, and a voting poll for the members to choose between 4 cars in that category. Additionally, each page had a discussion where you could post your thoughts, ideas, and comments on cars in that category and see other people's comments. The page I worked on was "Student Cars", which had examples of and discussions on the cars that high school students typically drive.

One of my coding accomplishments in Sprint 3 was learning how backend works and how frontend connects to a backend via an API. An API takes in a command from the frontend, processes it through the backend, and displays the result in a structured and user-friendly format (in our case, JSON). For our project, I focused on users adding comments to the discussion and the comments being sent to our backend database. I was initially going to make users submit their name, which car brand they liked best, and why, but Weston told me to keep the discussion pages uniform. Weston, Arnav, and Lars (the other members if my group) only had users add their thoughts, ideas, and comments in one submission, so I stuck to that as well and developed it so that the discussion became a user-friendly UI and the comment submission could be saved in backend.

Through Sprint 3, I not only enhanced my knowledge on how to develop frontend and style the page, but also learned about backend, databases and storage of data, what an API is, how an API connects the frontend to the backend, and how a backend and API contributes to the usability, features, and / or convenience of a website. I also collaborated with my teammates to learn about backend and API usage, as well as to develop our car debates page.

## 2018 AP CSP MC Practice Exam

Here is my performance in each section of the exam:

<img src="{{ site.baseurl }}/images/2018mc1.png">
<img src="{{ site.baseurl }}/images/2018mc2.png">

The topics that I did not do well on were 2.2 (Data Compression), 3.9 (Developing Algorithms), 3.13 (Developing Procedures), and 3.17 (Algorithmic Efficiency). I need to work on these topics and improve in order to perform better on future MCQs and the AP Exam.

However, the topics that I performed well on were 1.4 (Identifying and Correcting Errors), 2.3 (Extracting Infornation from Data), 3.12 (Calling Procedures), and 5.1 (beneficial and Harmful Effects). These are areas of less concern and I only need to review and do some practice on these topics.

I reflected on my performance using the graphs and tables below. These will also help me prepare for future MC exams.

### What did I learn?

- Taking this quiz helped me understand the structure of AP exam questions and key topics such as abstraction, algorithms, code functions, and impacts of computing on society. Questions within those topics seem very interesting and I will Here is the percentage of questions I got wrong in each category (out of the questions I got wrong):

- Because I had learned about the fundamentals of programming, I was easily able to understand more than half of the questions, such as the ones for analyzing code and the functions of code snippets, using data in real world scenarios, and even some for binary code usage.

On a larger perspective, my performance in terms of each big idea was:

<img src="{{ site.baseurl }}/images/2018mcblueandred.png">

The overall trend for the units was that the more questions there were, the more questions I got wrong in that unit. However, I did exceptionally poor in big idea 3, getting almost 1/3 of the questions wrong, and exceptionally well in big ideas 1 and 5, getting less than 1/4 of the questions wrong.

Here is my overall performance on the 14 questions I got wrong, separated by each big idea:

<img src="{{ site.baseurl }}/images/2018mcwrongperf.png">

For Big Idea 2, the questions for topic 2.2 (Data Compression) were tough to understand, and I need to study 2.2 in order to perform better on future questions. Similarly, I did not understand the concept of the question for 3.9, 3.13, and 3.17 in Big Idea 3, since they covered topics such as abstraction, procedual analysis, and algorithms.

- In the future, I hope to get a lot more practice with MC questions through online sites that provide questions, searching previous collegeboard exams and practice material, and getting a prep book, which will help me master the 5 big ideas of AP CSP

## Corrections:

Here are some of the questions I reflected on to improve for future mc exams:

### Topic 2.2 Data Compression

Q #24. Byte pair encoding is a data encoding technique. The encoding algorithm looks for pairs of characters that appear in the string more than once and replaces each instance of that pair with a corresponding character that does not appear in the string. The algorithm saves a list containing the mapping of character pairs to their corresponding replacement characters.

For example, the string "THIS_IS_THE_BEST_WISH" can be encoded as "%#_#_%E_BEST_W#H" by replacing all instances of "TH" with "%" and by replacing all instances of "IS" with "#".

Which of the following statements about byte pair encoding is true?

- The correct answer is "Byte pair encoding is an example of a lossless transformation because an encoded string can be restored to its original version." My answer was "Byte pair encoding is an example of a lossy transformation because some pairs of characters are replaced by a single character" which is incorrect because a lossy transformation is where data is degraded and severely compressed so that small unimportant details are permanently deleted, but a lossless transformation is where all of the data can be retained to its original form but is not able to compress as much. Because encoding also allows for data to be "decoded" or restored to its original form through a code, and byte pair encoding shortens information while encoding it, byte pair encoding is an example of a lossless transformation.

Q #25. (Continuation of 24) For which of the following strings is it NOT possible to use byte pair encoding to shorten the string’s length?

- The correct answer is *LEVEL_UP* because it does not have any repeating instances of two characters. When there is such an instance, byte pair encoding can be used to compress the code, which is the case for my answer. My answer was *BANANA*, which, although is a short word, has one instance of the word "NA" repeating.

### Topic 3.6 Data Compression

Q #5. A programmer is creating an algorithm to set the value of One word, ticket Price based on the information in the table. The programmer uses the integer  variable age for the age of the moviegoer. The Boolean variable One word, is 3 D is true when the movie is 3-D and false otherwise.

Which of the following code segments correctly sets the value of One word, ticket Price ?

- The correct answer was C, where ticketprice would increase by 5 IF the movie was 3D. I selected the answer where ticketprice goes up by 5 regardless of if the movie was 3D or not (else: ticketprice = ticketprice + 5). This shows that I analyzed the code snippet incorrectly and should have considered all factors that should be in the code before sleecting the corresponding code snippet.

### Topic 3.9 Developing Algorithms

Q #22. A student is creating a procedure to determine whether the weather for a particular month was considered very hot. The procedure takes as input a list containing daily high temperatures for a particular month. The procedure is intended to return true if the daily high temperature was at least 90 degrees for a majority of days in the month and return false otherwise.

Which of the following can be used to replace missing code so that the procedure works as intended?

- The correct answer was counter > 0.5 * total. I put total > 0.5 * counter, which will always return true since the total amount will always be greater than half the amount of times the value was greater than 90, and thus incorrect. The correct code is correct as it returns true only when counter makes up more than half of the total values. 

### Topic 3.10 Lists

Q #50. The procedure below searches for the value target in list. It returns true if target is found and returns false otherwise.

Which of the following are true statements about the procedure?

I. It implements a binary search.

II. It implements a linear search.

III. It only works as intended when list is sorted.

- The correct answer is II only because it implements a linear search, since it sequentially goes through each element in the list until it finds the target element. It does not undergo a binary search since the list would need to be sorted and preferably very large in order for binary search to be 100% efficient. Similarly, the list does not need to be sorted because the list implements a linear search and the order of the items does not matter to search for the targeted item. This is also why my answer (II and III) is incorrect.

### Topic 3.13 Developing Procedures

Q #54. A programmer notices the following two procedures in a library. The procedures do similar, but not identical, things.

Procedure Square(n) returns the value N squared.
Procedure Cube(n) returns the value N raised to the third power.

Which of the following procedures is a generalization of the procedures described above?

- The correct answer is Procedure Power(n,m) which returns n^m. This is because square and cube are examples of numbers raised to a power, and a more general program would be to be able to raise any number to any power. In contrast, Fourth(n) returns the fourth power of the function, which is only a continuation of the previous two programs rather than generalizing the two programs as one.

Q #60. Which of the following is a way in which a programmer can use abstraction to manage the complexity of a program?

- My answer is Replacing several lines of documentation with a single line of documentation, which only moves the lines of a program to the same line (it does not improve the program complexity). In contrast, Replacing each instance of repeated code with a call to a procedure can allow a programmer to minimize the lines of code by creating a shortcut for functions that serve similar purposes. For instance, if you need to find the prime numbers in a list, instead of repeating the code each time, you can create a function primeNumbers() that can be used for every instance a program needs to find a list of prime numbers.

### Topic 3.17 Algorithmic Efficiency

Q #30. A video-streaming service maintains a database of information about its customers and the videos they have watched.

The program below analyzes the data in the database and compares the number of viewers of science fiction videos to the number of viewers of videos of other genres. It uses the procedure Analysis which returns the number of unique users who viewed videos of a given category in the past year. The Analysis procedure takes approximately 1 hour to return a result, regardless of the number of videos of the given genre. All other operations happen nearly instantaneously.

Which of the following best approximates the amount of time it takes the program to execute?

- The correct answer is 5 hours because Analysis is called once before the loop and 4 times within the loop. My answer, 2 hours, assumes Analysis was called once within the loop, which is incorrect as the loop repeats 4 times. I need to analyze the code snippet more carefully to check how many times a loop will repeat so I can answer future questions that are similar.

### Topic 5.6 Safe Computing

Q #47. In public key cryptography, the sender uses the recipient’s public key to encrypt a message. Which of the following is needed to decrypt the message?

- The correct answer is the recipient's private key because in public cryptography, a message is encrypted with a recipient’s public key and decrypted with the recipient’s private key. Thus, my answer is incorrect. 

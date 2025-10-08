---
toc: True
comments: False
layout: post
title: BI 4.1 Internet - Web Server
description: Quick launch into Flask, sending and receiving data from a web server.
courses: {'csp': {'week': 14}}
type: ccc
categories: ['CSP Lessons']
---

## Introduction

Welcome to this journey into the world of web servers and the Flask framework! In the previous weeks, you've successfully set up a web server using GitHub Pages, converting Jupyter Notebooks into Markdown for a seamless online presentation. Today, we'll take that knowledge to the next level as we dive into creating your very own web server using Flask.

### Understanding Web Servers
What is a Web Server?

Traditionally, we had librarians at libraries that would help you find books or information. Today in the digital world, thousands upon thousands of home pages, search engines, and digital archives have been built using web servers.

### GitHub Pages vs. Flask

You've already experienced a form of web server through GitHub Pages. Think of GitHub Pages as a library that has established rules for publishing Markdown notes and Jupyter Notebooks neatly on a bookshelf.

Now, let's introduce Flask, your personal web server. Flask can create and manage any type of content, including customizing everything according to your preferences, and even serve additional information (like a database with APIs).

The Flask Framework
Flask is a micro web framework written in Python. It's designed to be minimal and easy to use, making it perfect for building web applications, APIs, and, yes, even your web server. Today, we will start with the basics of Flask and see how it empowers you to create and manage web content.

##  Our Goals for Today
Here's what we'll accomplish in this session:

- Create a minimal Flask server.
- Explore the Python/Flask process.
- Access data from our Flask server using Python.
- Access data from our Flask server using JavaScript.
- Learn how to stop the Python/Flask process gracefully.



### Install required libraries
These libraries are required to run and interact with the Python web server.


```python
!pip install flask flask-cors requests
```

    Collecting flask
      Using cached flask-3.1.0-py3-none-any.whl.metadata (2.7 kB)
    Collecting flask-cors
      Using cached Flask_Cors-5.0.0-py2.py3-none-any.whl.metadata (5.5 kB)
    Collecting requests
      Using cached requests-2.32.3-py3-none-any.whl.metadata (4.6 kB)
    Collecting Werkzeug>=3.1 (from flask)
      Using cached werkzeug-3.1.3-py3-none-any.whl.metadata (3.7 kB)
    Collecting Jinja2>=3.1.2 (from flask)
      Using cached jinja2-3.1.4-py3-none-any.whl.metadata (2.6 kB)
    Collecting itsdangerous>=2.2 (from flask)
      Using cached itsdangerous-2.2.0-py3-none-any.whl.metadata (1.9 kB)
    Collecting click>=8.1.3 (from flask)
      Using cached click-8.1.7-py3-none-any.whl.metadata (3.0 kB)
    Collecting blinker>=1.9 (from flask)
      Using cached blinker-1.9.0-py3-none-any.whl.metadata (1.6 kB)
    Collecting charset-normalizer<4,>=2 (from requests)
      Using cached charset_normalizer-3.4.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (34 kB)
    Collecting idna<4,>=2.5 (from requests)
      Using cached idna-3.10-py3-none-any.whl.metadata (10 kB)
    Collecting urllib3<3,>=1.21.1 (from requests)
      Using cached urllib3-2.2.3-py3-none-any.whl.metadata (6.5 kB)
    Collecting certifi>=2017.4.17 (from requests)
      Using cached certifi-2024.8.30-py3-none-any.whl.metadata (2.2 kB)
    Collecting MarkupSafe>=2.0 (from Jinja2>=3.1.2->flask)
      Using cached MarkupSafe-3.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.0 kB)
    Using cached flask-3.1.0-py3-none-any.whl (102 kB)
    Using cached Flask_Cors-5.0.0-py2.py3-none-any.whl (14 kB)
    Using cached requests-2.32.3-py3-none-any.whl (64 kB)
    Using cached blinker-1.9.0-py3-none-any.whl (8.5 kB)
    Using cached certifi-2024.8.30-py3-none-any.whl (167 kB)
    Using cached charset_normalizer-3.4.0-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (143 kB)
    Using cached click-8.1.7-py3-none-any.whl (97 kB)
    Using cached idna-3.10-py3-none-any.whl (70 kB)
    Using cached itsdangerous-2.2.0-py3-none-any.whl (16 kB)
    Using cached jinja2-3.1.4-py3-none-any.whl (133 kB)
    Using cached urllib3-2.2.3-py3-none-any.whl (126 kB)
    Using cached werkzeug-3.1.3-py3-none-any.whl (224 kB)
    Using cached MarkupSafe-3.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (23 kB)
    Installing collected packages: urllib3, MarkupSafe, itsdangerous, idna, click, charset-normalizer, certifi, blinker, Werkzeug, requests, Jinja2, flask, flask-cors
    Successfully installed Jinja2-3.1.4 MarkupSafe-3.0.2 Werkzeug-3.1.3 blinker-1.9.0 certifi-2024.8.30 charset-normalizer-3.4.0 click-8.1.7 flask-3.1.0 flask-cors-5.0.0 idna-3.10 itsdangerous-2.2.0 requests-2.32.3 urllib3-2.2.3


### Start Web Server
This Python code provides a simple server with an accessible API.

Note: Jupyter magic commmand `%%python --bg` that follows runs the server in background.  This enables us to continue interacting with the subsequent Notebook cells.


```python
%%python --bg

from flask import Flask, jsonify
from flask_cors import CORS

# initialize a flask application (app)
app = Flask(__name__)
CORS(app, supports_credentials=True, origins='*')  # Allow all origins (*)

# ... your existing Flask

# add an api endpoint to flask app+
@app.route('/api/shaurya')
def get_shaurya():
    # start a list, to be used like a information database
    InfoDb = []

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "Shaurya",
        "LastName": "Singh",
        "DOB": "November 18",
        "Residence": "San Diego",
        "Email": "shauryasinghus@gmail.com",
        "Owns_Cars": ["2015-Fusion", "2011-Ranger", "2003-Excursion", "1997-F350", "1969-Cadillac"]
    })

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "John",
        "LastName": "Doe",
        "DOB": "January 1",
        "Residence": "Shanghai",
        "Email": "jdoe1@gmail.com",
        "Owns_Cars": ["2024-Accord"]
    })
    
    return jsonify(InfoDb)

# add an HTML endpoint to flask app
@app.route('/')
def say_hello():
    html_content = """
    <html>
    <head>
        <title>Hellox</title>
    </head>
    <body>
        <h2>Hello, World!</h2>
    </body>
    </html>
    """
    return html_content

if __name__ == '__main__':
    # starts flask server on default port, http://127.0.0.1:5001
    app.run(port=5001)
```

### Explore the Python/Flask process with Linux
This script discovers the running flask process on your machine using Linux commands.

1. lsof - list open files
2. `lsof` and `awk` return the process id, so `ps` can list details, the vericle bar is called a `pipe`.  A pipe flows output from one command to the next.
3. `curl` is a Linux utiltity that is easiest way to test if web server is responding


```python
%%script bash

# After app.run(), see the the Python open files on port 5001
echo "Python open files on port 5001" 
lsof -i :5001
# see the the Python process 
echo
echo "Python process"
lsof -i :5001 | awk '/Python/ {print $2}' | xargs ps
# show ontent of the Python server using curl
echo
echo "Content of the Python root endpoint (aka /), using curl",  
curl http://localhost:5001/


```

### Access data from our Flask server using Python
The code block below shows alternate ways to access the Web Server.
1. Import requests and use it to obtain response from endpoints
2. The response is a Python object that contains status codes and data
3. The data can be in different forms, we will be focussed on JSON responses in Full-Stack.


```python
import requests
from IPython.display import HTML, display

# call api root endpoint (aka '/'), often called home page
response = requests.get('http://127.0.0.1:5001/')
# output response in different forms
print("Print Status Message:", response)
print("\nPrint Raw HTML:\n", response.text)
display(HTML(response.text))

# call unknown api endpoint
response = requests.get('http://127.0.0.1:5001/unknown-page')
print("Print Status Message:", response)
```


```python
import requests
# an api endpoint most commonly returns JSON data
response = requests.get('http://127.0.0.1:5001/api/data')
response.json()
```

### Access data from our Flask server using JavaScript
This sample is very similar to Full-Stack as the JavaScript is running through Jupyter and the Web server is a Python Process running on our machine (local server).

1. HTML is used to setup basics of a table
2. The script block, has javascript fetch that passes endpoint (url) and options.  The options are critical to communicating request requirements.
3. Similar to python examples, data is extracted and that data is written to the document, which is what is viewable to the user as the page is rendered.  Headings are static in the document, but rows are dynamically extracted according to the information contained in the server.


```python
%%html

<h1>Access data from our Flask server using JavaScript</h1>

<p>This code extracts data "live" from a local Web Server with JavaScript fetch.  Additionally, it formats the data into a table.</p>

<!-- Head contains information to Support the Document -->


<!-- HTML table fragment for page -->
<table id="demo" class="table">
  <thead>
      <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Residence</th>
      </tr>
  </thead>
  <tbody id="result">
    <!-- javascript generated data -->
  </tbody>
</table>

<script>
  // prepare HTML result container for new output
  let resultContainer = document.getElementById("result");
  
  // prepare URL
  url = "http://127.0.0.1:5001/api/data";

  // set options for cross origin header request
  let options = {
    method: 'GET', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'include', // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json',
    },
  };

  // fetch the API
  fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors and display
      if (response.status !== 200) {
          console.error(response.status);
          return;
      }
      // valid response will contain json data
      response.json().then(data => {
          console.log(data);
          for (const row of data) {
            // tr and td build out for each row
            const tr = document.createElement("tr");
            const firstname = document.createElement("td");
            const lastname = document.createElement("td");
            const residence = document.createElement("td");
            // data is specific to the API
            firstname.innerHTML = row.FirstName; 
            lastname.innerHTML = row.LastName; 
            residence.innerHTML = row.Residence; 
            // this builds each td into tr
            tr.appendChild(firstname);
            tr.appendChild(lastname);
            tr.appendChild(residence);
            // add HTML to container
            resultContainer.appendChild(tr);
          }
      })
  })
  
</script>


```

### Stop the Python/Flask process
This script ends Python/Flask process using pipes to obtain the python process.  Then echo the python process to `kill -9`.  


```python
%%script bash

python_ps=$(lsof -i :5001 | awk '/Python/ {print $2}')
echo "Killing python process with PID: $python_ps"
echo $python_ps | xargs kill -9
```

## Hacks
Edit, stop and start the web server.
- Add to the Home Page
- Add your own information to the Web API
- Use from Template to start your own Team Flask project https://github.com/nighthawkcoders/flocker_backend

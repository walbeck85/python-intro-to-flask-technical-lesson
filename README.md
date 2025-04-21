# Technical Lesson: Introduction to Flask

In this lesson, we will explore how to build routes within python through using Flask.

## The Scenario

You are working for a social media company. As a part of that company they want you to begin their internal api for requesting information from users. Using your knowledge of routes they want you to get a standard route for the main page as well as a user specific route for getting a particular username

### Developer Tasks

* Initialize flask
* Build ‘/’ route
* Build ‘/’ username routeFrame the lesson by using problem-solving with the established process.

## Tools & Resources

- [GitHub Repo](https://github.com/learn-co-curriculum/python-intro-to-flask-technical-lesson)
- [Quick Start - Flask](https://flask.palletsprojects.com/en/2.2.x/quickstart)
- [Chapter 2. Basic Application Structure - Flask Web Development, 2nd Edition](https://learning.oreilly.com/library/view/flask-web-development/9781491991725/ch02.html#idm140583868985008)
- [A Minimal Application - Flask](https://flask.palletsprojects.com/en/2.2.x/quickstart/#a-minimal-application)

## Instructions

### Set Up

Before we begin coding, let's complete the initial setup for this lesson. For this lesson, you will need to use the provided GitHub repository link.

* Fork and Clone
  * Fork the repository to your GitHub account.
  * Clone the forked repository to your local machine.
* Open and Run File
  * Open the project in VSCode.
  * Run pipenv install to install all necessary dependencies.
  * Run pipenv shell to open instance of python shell

### Task 1: Define the Problem

You are working for a social media company. As a part of that company they want you to begin their internal api for requesting information from users. Using your knowledge of routes they want you to get a standard route for the main page as well as a user specific route for getting a particular username

<br />

* Developer tasks
  * Initialize flask
  * Build ‘/’ route
  * Build ‘/’ username route

### Task 2: Determine the Design

Determine Routes
* /
* /<username>

### Task 3: Develop, Test, and Refine the Code 

#### Step 1: Create a Feature Branch

```bash
git checkout -b flask_routes
```

#### Step 2: Initialize Flask

Double check that you have run your install and shell command. When initializing flask ensure it is imported so we can use the Flask class.
<br />
All code changes will happen in server/app.py

```python
from flask import Flask

app = Flask(__name__)
```

The Flask class constructor only requires the name of the primary module or package to be interpreted as the application. Flask uses this to figure out where the application is and where its important files will be. As some of these will not be .py files and might not have any .py files in their directory, Flask needs to set up an application structure that allows it to see everything.
<br />
For the purposes of this lab, this argument will always be __name__, which refers to the name of the current module.

#### Step 3: Building a Route

When clients send requests to our application's server, they are forwarded to our Flask application instance. This instance will receive requests for many different resources, located at different Uniform Resource Locations (URLs). To map these URLs to Python functions, we need to define routes.
<br />
Routing is the association of URLs and the code that should execute when a request comes in for that URL. Routing isn't just a Python concept- JavaScript, Java, Ruby, and even newer languages like Rust and Go use routes to direct requests to the appropriate backend code.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Welcome to my page!</h1>'
```

The easiest way to define routes with Flask is through use of the @app.route decorator:
<br />
Remember that decorators are functions that take functions as arguments and return them decorated with new features. @app.route registers the index() function with the Flask application instance app. The @app.route() decorator is an instance method that modifies app, creating a rule that requests for the base URL (/) should show our index: a page with a header that says "Welcome to my app!" 

#### Step 4: Variable Routes

Navigate to your favorite social media site and take a look at the URL. The base will represent the index or homepage for the application.
<br />
Navigate to a user profile and take another look at the URL.
"google.com" is clearly a fixed portion of the URL- it's everywhere! There are other pieces, though, that it wouldn't make sense to hard-code into our application. "NASA", for instance, is the username for one out of millions of users on the site. Managing views for that many users would be impossible! 
<br />
Lucky for us, Flask allows us to parameterize different parts of our routes. When we interpolate these into strings or use them to retrieve records from a database, we can create flexible, dynamic applications:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Welcome to my page!</h1>'

@app.route('/<string:username>')
def user(username):
    return f'<h1>Profile for {username}</h1>'
```

Anything included in the route passed to the app.route decorator with angle brackets <> surrounding it will be passed to the decorated function as a parameter (in this case username). We can make sure that the username is a valid string, int, float, or path by specifying it in the route.

#### Step 5: Testing using Flask

Now that our routes are built we can go ahead and test the application quite easily. We can go ahead and run the following lines in our terminal (make sure we are in our pipenv virtual environment):

```bash
export FLASK_APP=app.py
export FLASK_RUN_PORT=5555
flask run
```

These lines will let us set up our flask to run with our python file and run on port 5555 (a commonly open port). Flask run will start our flask instance. We will only need to run flask run from here on out.
<br />
Navigate to http://127.0.0.1:5555 and confirm it is working.
<br />
Navigate to http://127.0.0.1:5555/mr-user to confirm our variable route is working (try changing that variable).

#### Step 6: Set Up Auto Run

This next step is optional but will provide lots of useful features and options. We can set up our app to trigger flask run after running the app (using python app.py) by setting up this method.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Welcome to my page!</h1>'

@app.route('/<string:username>')
def user(username):
    return f'<h1>Profile for {username}</h1>'

if __name__ == '__main__':
    app.run(port=5555, debug=True)
```

We set up at the bottom of our app app.run and this can let us control useful features such as an auto rerun. By using the debug line we can set our app up so that it will cause the server to restart when we save, whereas previously when testing if we wanted to see a change we make apply to our server we would need to restart the server by exiting and rerunning flask.
<br />
Once you have verified that our routes work, commit changes:

```bash
git commit -am "Finish / and username route"
```

#### Step 7: Push changes to GitHub and Merge Branches

* Push the branch to GitHub:

```bash
git push origin flask_routes
```

* Create a Pull Request (PR) on GitHub.

* Merge the PR into main after review.

* Pull the new merged main branch locally and delete merged feature branch (optional):

```bash
git checkout main
git pull origin main

git branch -d flask_routes
```

* If the last command doesn’t delete the branch, it’s likely git is not recognizing the branch as having been merged. Verify you do have the merged code in your main branch, then you can run the same command but with a capital D to ignore the warning and delete the branch anyway.

```bash
git branch -D flask_routes
```

### Task 4: Document and Maintain

Best Practice Documentation Steps:
* Add comments to code to explain purpose and logic
  * Clarify intent / functionality of code to other developers
* Add screenshot of completed work included in Markdown in README.
* Update README text to reflect the functionality of the application following https://makeareadme.com.
* Delete any stale branches on GitHub
* Remove unnecessary/commented out code
* If needed, update git ignore to remove sensitive data

## Considerations

* Route Priority
  * Flask uses Werkzeug to handle routing, and it orders routes based on how many variable parts are in the route.
  * /test has no variable parts, while /<to> does, so it'll try to match /test first, regardless of what order you defined them.
* Ports
  * A computer has many different ports, most of the time 5555 is an open port so commonly used for backend applications.
* Default Route
  * The default route should be considered ‘/’, most api developers will add some route for ‘/’ that will overview their api.


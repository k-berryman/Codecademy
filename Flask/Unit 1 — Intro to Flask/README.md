# Intro to Flask
Codecademy Notes (https://www.codecademy.com/learn/learn-flask)

Learning the basics

----

## Intro to Web Apps with Flask
Flask is a Python web micro-framework. In this course, we'll create fully-featured web apps with Flask.

----

## What is the back-end?
### Storing Data
The back-ends of websites typically include a database to store information. Relational databases store info in tables. Non-relational aka NoSQL databases use other systems like key-value pairs or a document storage model. SQL (Structured Query Language) is a programming language for relational databases. Examples of relational databases are MySQL & Postgres. Examples of NoSQL databases are MongoDB & Redis.

The back-end needs the ability to access, change, and analyze database data

### What's an API?
API stands for Application Program Interface. To have consistent ways of interacting with data, a back-end can use a web API. 

A web API is a collection of predefined ways of interacting with a web application's data, often through a HTTP request-response cycle. Unlike the HTTP request from client to server when a url load, this type of request indicates how it would like to interact with a web app's data, and it receives some data back as a response.

Database  <——> Web API (CRUD)

CRUD — Create new data, read data, update data, delete data)

Some APIs are open to the public.

### Authorization & Authentication
Our server shall handle this.

**Authentication** is the process of validating the identity of a user. "Who is this? Is it really you?" One example is usernames/passwords as credentials stored in the back-ends database. We can also use external log-in resources such as logging in with Google.

**Authorization** dictates which users have access to which resources and actions. "What is this user allowed to see/do?" Think of admin-access vs. intern-access.

Our back-end needs Authentication & Authorization in our server-side logic to create *secure, personalized, & dynamic* content.

### Different Back-end Stacks
Various programming languages can make a back-end.
Many developers use frameworks as a collection of tools that shape the organization of our back-end. Examples are Express, Flask, Django, Spring, Ruby on Rails, etc.

The collection of technologies used to create the front-end and back-end is called the stack. Think of a *full-stack* developer.

The MEAN stack uses 
**M**ongoDB for the database
**E**xpress for the back-end
**A**ngular for the front-end
**N**ode

The LAMP stack uses
**L**inux
**A**pache
**M**ySQL
**P**HP

### Review
  * The front-end is HTML, CSS, JS, & static assets sent to a web browser
  * A web server is a process running on our computer that listens for incoming requests over the internet and sends back responses
  * Manipulating data (CRUD) 
  * Databases
  * The server-side of a web app, sometimes called the application server, handles important tasks such as authentication & authorization
  * The back-end of a web app often has a web API which helps interact with the app's database through HTTP requests and responses
  * The front-end and back-end together make the tech stack

Now we have a basic knowledge of server-side development and what the back-end is!

----

## HTTP Requests Article

Sample text

----

## Build Your First Flask App (Lesson)

Sample Text

----

## Build Your First Flask App (Quiz)

Sample text

----

## Adopt a Pet (Project)

Sample text

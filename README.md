# Lab1 - Public Domain Book-Sharing Platform
### Răzvan Fișer FAF-203

## 1. Application Suitability for Microservices
The application is suitable for Microservices Architecture because it both requires to carry a relatively large ammount of data (through the form of PDFs) at one point in time and serve many users simultaneously. Thus, we want our app to support large loads of data and be scalable, which Microservices does well. 

Moreover, we might want to use a different language for handling PDFs (e.g. Python) and Microservices are wonderful for when you want to choose the most well-suited technology stack for each service.

A notable example of a similar web application that uses microservices is [Internet Archive](https://archive.org/), which is a non-profit library for free movies, software, music and <b>books</b>.

## 2. Service Boundaries
The project should contain three microservices with the following functionalities:
1. Account Service - handles user authentification, session tracking etc.;
2. Search Service - handles searching for books by certain tags and filters 
such as title, date, author etc.;
3. Download/Upload Service - handles the uploading and downloading of books in PDF format.

Below  you can see the corresponding System Architecture Diagram for the above-mentioned microservices:

![System Architecture Diagram](./system%20architecture.png?raw=true "System Architecture Diagram")

## 3. Technology Stack and Communication Patterns
For this project the technology stack will be divided as follows:
* <b>Elixir</b> - for implementing the Account- and Search Services respectively. The <b>message queue</b> communication patterns will be used for these since this is what Elixir uses by default;

* <b>Python's Flask Framework </b> - Python and Flask will be used for handling the downloading/uploading of the books, since Python has a number of libraries which can handle/manipulate PDFs, which could potentially prove useful. For this a <b>RESTful API</b> will be adopted.

## 4. Data Management

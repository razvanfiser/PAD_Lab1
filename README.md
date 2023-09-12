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
### 4.1. Databases
As seen in the System Architecture Diagram, the Account Service will store all of its data related to the users into the Account Database. The Search- and Download/Upload Services will communicate with the Book Database. All communication with the databases will be done through RESTful APIs.
### 4.2. Endpoins
#### Account Service
```json
POST /signup/
    data = {
        "username": "{username}",
        "password": "{password}",
        "email": "{email}"
    }

    RESPONSE:
        {
            "status": 200
        }

POST /login/
    data = {
        "username": "{username}",
        "password": "{password}"
    }

    RESPONSE:
        {
            "Authorization": "{session_id}"
        }

DELETE /deleteacc/
    headers = {"Authorization": "{session_id}"}
    data = {
        "username": "{username}",
        "password": "{password}"
    }

    RESPONSE:
    {
        "status": 200
    }

```

#### Search Service
```json
GET /author/

GET /book/

```

#### Upload/Download Service
```json
GET /download/{book_id}/
    headers = {"Authorization": "{session_id}"}

    RESPONSE:
        {
            "name": "Russia's Catacomb Saints",
            "author": "St. Herman of Alaska Brotherhood",
            "category": "religion",
            "url": "download url"
        }

POST /upload/
    headers = {"Authorization": "{session_id}"}
    data = {
        "name": "{name}",
        "author": "{author}",
        "category": "{category}",
        "tags": []
        "url": "download url"
    }

    RESPONSE:
        {
            "status": 201
        }
```
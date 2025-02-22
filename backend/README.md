# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createbd trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Run the Server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## To Do Tasks

These are the files you'd want to edit in the backend:

1. `backend/flaskr/__init__.py`
2. `backend/test_flaskr.py`

One note before you delve into your tasks: for each endpoint, you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle `GET` requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle `GET` requests for all available categories.
4. Create an endpoint to `DELETE` a question using a question `ID`.
5. Create an endpoint to `POST` a new question, which will require the question and answer text, category, and difficulty score.
6. Create a `POST` endpoint to get questions based on category.
7. Create a `POST` endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a `POST` endpoint to get questions to play the quiz. This endpoint should take a category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422, and 500.

## API Documentation

### Getting Started
- Base URL: This App is currently in develoment stage. It is not hosted on a web server. It can only be run locally. The backend is hosted at the default localhost address: `http://127.0.0.1:5000/` which is set as a proxy in the frontend configuration.
- Authentication: This version of the application does not require authentication or API keys.

### Error Handling
- Errors are returned as JSON object in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return four error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable
- 500: Internal Server error 

### Endpoints
#### GET/categories
- General: Returns all the available categories
- URI: `curl http://127.0.0.1:5000/categories`
- Response:

```
{
    categories: {
        1: "Science",
        2: "Art",
        3: "Geography",
        4: "History",
        5: "Entertainment",
        6: "Sports"
    },
    success: true
}
```
### GET /questions
- General: Returns a list of paginated questions, 10 questions per page.
- URI: http://127.0.0.1:5000/questions
- Request Arguments: limit, page
- Sample: `curl http://127.0.0.1:5000/questions`
- Response:
```
{
    "categories":{
      "1":"Science",
      "2":"Art",
      "3":"Geography",
      "4":"History",
      "5":"Entertainment",
      "6":"Sports"
    },
    "questions":[
      {
        "answer":"Tom Cruise",
        "category":5,
        "difficulty":4,
        "id":4,
        "question":"What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
      },
      {
        "answer":"Maya Angelou",
        "category":4,
        "difficulty":2,
        "id":5,
        "question":"Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
      },
      {
        "answer":"Edward Scissorhands",
        "category":5,
        "difficulty":3,
        "id":6,
        "question":"What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      },
      {
        "answer":"Muhammad Ali",
        "category":4,
        "difficulty":1,
        "id":9,
        "question":"What boxer's original name is Cassius Clay?"
      },
      {
        "answer":"Brazil",
        "category":6,
        "difficulty":3,
        "id":10,
        "question":"Which is the only team to play in every soccer World Cup tournament?"
      },
      {
        "answer":"Uruguay",
        "category":6,
        "difficulty":4,
        "id":11,
        "question":"Which country won the first ever soccer World Cup in 1930?"
      },
      {
        "answer":"George Washington Carver",
        "category":4,
        "difficulty":2,
        "id":12,
        "question":"Who invented Peanut Butter?"
      },
      {
        "answer":"Lake Victoria",
        "category":3,
        "difficulty":2,
        "id":13,
        "question":"What is the largest lake in Africa?"
      },
      {
        "answer":"The Palace of Versailles",
        "category":3,
        "difficulty":3,
        "id":14,
        "question":"In which royal palace would you find the Hall of Mirrors?"
      },
      {
        "answer":"Agra",
        "category":3,
        "difficulty":2,
        "id":15,
        "question":"The Taj Mahal is located in which Indian city?"
      }
    ],
      "selected_page":1,
      "success":true,
      "total_questions":22
}
```

### POST /questions
- General: Insert or create a new question
- URI: http://127.0.0.1:5000/questions
- Request Arguments: Question, answer, category, and difficulty
- Sample: `curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question": "What is the colour of sky", "answer": "blue","difficulty": 1,"category": 2}'`

- JSON File format:
```
{
  "id": 10,
  "question": "What is the colour of sky"
  "answer": "blue",
  "category": "2",
  "difficulty": 1,    
}
```
- Sample Response:
```
{
  "question": {
      "answer": "blue",
      "category": "2",
      "difficulty": 1,
      "id": 17,
      "question": "What is the colour of sky"
  },
  "success": true
}
```

### POST /search
- General: Find a question by searching through a string pattern within the `question` body
- URI: http://127.0.0.1:5000/search
- Sample: `curl -X POST http://127.0.0.1:5000/search`
- Request Arguments: searchTerm 
- Response:
```
{
  "success": true,
  "questions": []
}
```

### DELETE /questions/<int:question_id>

- General: Delete a question with a given ID
- URI: http://127.0.0.1:5000/questions/<int:question_id>
- Sample: `curl -X DELETE http://127.0.0.1:5000/questions/27`
- Request Arguments: None
- Response:
```
{
  "deleted_id": 27, 
  "success": true
}
```

### GET /categories/<int:category_id>/questions
- General: Returns a list of all questions in a given category, specified by a category ID
- URI: http://127.0.0.1:5000/categories/<int:category_id>/questions
- Sample: `curl http://127.0.0.1:5000/categories/1/questions`
- Response:
```
{
  "questions": [
    {
      "answer": "The Liver", 
      "category": 1, 
      "difficulty": 4, 
      "id": 20, 
      "question": "What is the heaviest organ in the human body?"
    }, 
    {
      "answer": "Alexander Fleming", 
      "category": 1, 
      "difficulty": 3, 
      "id": 21, 
      "question": "Who discovered penicillin?"
    }, 
    {
      "answer": "Blood", 
      "category": 1, 
      "difficulty": 4, 
      "id": 22, 
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ], 
  "success": true
}
```

### POST /quizzes
- General: Returns a list of questions to play the quiz
- URI: http://127.0.0.1:5000/quizzes
- Sample: `curl -X POST http://127.0.0.1:5000/quizzes`
- Request Arguments: quiz_category, previous_questions
- Response:
```
{
  "success": true,
  "question": []
}
```

## Testing

To deploy the tests, run

```bash
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

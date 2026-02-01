
# GET Method in FastAPI

## 📌 What is GET Method?
The **GET method** is an HTTP request used to **retrieve (read) data** from a server.  
It does **not modify** data on the server and is considered a **safe and idempotent** operation.

---

## 🚀 GET Method in FastAPI
In FastAPI, the GET method is used to:
- Fetch data from a database
- Retrieve user information
- Return predictions or results
- Read resources without changing them

---

## 🧠 Basic Syntax
```python
from fastapi import FastAPI

app = FastAPI()

MOVIES = [
    {"title": "Inception", "director": "Christopher Nolan", "genre": "Sci-Fi"},
    {"title": "The Godfather", "director": "Francis Ford Coppola", "genre": "Crime"},
    {"title": "Spirited Away", "director": "Hayao Miyazaki", "genre": "Animation"},
    {"title": "Parasite", "director": "Bong Joon-ho", "genre": "Thriller"},
    {"title": "Pulp Fiction", "director": "Quentin Tarantino", "genre": "Drama"},
]
@app.get("/movies")
def read_all_movies():
    return {"movies": MOVIES}

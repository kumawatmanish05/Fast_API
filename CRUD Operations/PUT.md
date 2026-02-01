# PUT Method in FastAPI

## 📌 What is PUT Method?

The **PUT method** is an HTTP request used to **update an existing resource completely** on the server.

In CRUD operations:

> **PUT = UPDATE**

If the resource already exists → it is replaced with new data.  
If it doesn’t exist → some APIs may create it (implementation dependent).

---

## Simple Language 

**1st we have to made a new pydantic model because in previous model all columns are compulsary
but in update we don't need all columns**

**2nd Url ke EndPoint me 2 cheze aayegi (1)Patient_id as a path parameter and (2)Request_body jisme ye bataya jayega ki konsa column update krna h** 

---

## 🧠 Simple Definition

**PUT request is used to update an existing resource by sending the full updated data to the server.**

---

## 🚀 Basic PUT Example in FastAPI

### 📁 main.py

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

# Fake database
users = [
    {"id": 1, "name": "Manish", "age": 20},
    {"id": 2, "name": "Rahul", "age": 22}
]

# Data Model
class User(BaseModel):
    name: str
    age: int

# PUT API (Update User)
@app.put("/users/{user_id}")
def update_user(user_id: int, user: User):
    for u in users:
        if u["id"] == user_id:
            u["name"] = user.name
            u["age"] = user.age
            return {"message": "User updated successfully", "user": u}

    raise HTTPException(status_code=404, detail="User not found")


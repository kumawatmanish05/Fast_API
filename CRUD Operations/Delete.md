# DELETE Method 

## 📌 What is DELETE Method?

The **DELETE method** is an HTTP request used to **remove an existing resource** from the server.

In CRUD operations:

> **DELETE = REMOVE**

It typically works with a **path parameter (ID)** to specify which record should be deleted.

---

## 🧠 Simple Definition

**DELETE request is used to delete a resource from the server using its unique identifier.**

---

## 🚀 Basic DELETE Example in FastAPI

### 📁 main.py

```python
from fastapi import FastAPI, HTTPException, status

app = FastAPI()

@app.delete('/delete/{patient_id}')
def delete_patient(patient_id: str):

    # load data
    data = load_data()

    if patient_id not in data:
        raise HTTPException(status_code=404, detail='Patient not found')
    
    del data[patient_id]

    save_data(data)

    return JSONResponse(status_code=200, content={'message':'patient deleted'})


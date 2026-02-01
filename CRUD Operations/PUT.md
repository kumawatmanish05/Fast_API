# PUT Method in FastAPI

## 📌 What is PUT Method?

The **PUT method** is an HTTP request used to **update an existing resource completely** on the server.

In CRUD operations:

> **PUT = UPDATE**

If the resource already exists → it is replaced with new data.  
If it doesn’t exist → some APIs may create it (implementation dependent).

---

## Simple Language 

**{1st} we have to made a new pydantic model because in previous model all columns are compulsary
but in update we don't need all columns**

**{2nd} Url ke EndPoint me 2 cheze aayegi (1)Patient_id as a path parameter and (2)Request_body jisme ye bataya jayega ki konsa column update krna h** 

---

## 🧠 Simple Definition

**PUT request is used to update an existing resource by sending the full updated data to the server.**

---

## 🚀 Basic PUT Example in FastAPI

### 📁 main.py

```python
from fastapi import FastAPI, Path , HTTPException , Query
from fastapi.responses import JSONResponse
from pydantic import BaseModel , Field , computed_field 
from typing import Annotated , Literal,Optional
import json

app = FastAPI()

# Data Model
class patientUpdate(BaseModel):
    name:Annotated[Optional[str],Field(default=None)]
    city:Annotated[Optional[str],Field(default=None)]
    age:Annotated[Optional[int],Field(default=None,gt=0)]
    gender:Annotated[Optional[Literal['male','female']],Field(default=None)]
    height:Annotated[Optional[float],Field(default = None,gt = 0)]
    weight:Annotated[Optional[float],Field(default=None,gt=0)]

# PUT API (Update User)
@app.put('/edit/{patient_id}')
def update_patient(patient_id :str, patient_update : patientUpdate) :

    data = load_data()

    if patient_id not in data:
        raise HTTPException(status_code = 404,detail='Patient Not found')
    
    existing_patient_info = data[patient_id]

    updated_patient_info = patient_update.model_dump(exclude_unset = True)

    for key ,value in updated_patient_info.items():
        existing_patient_info[key] = value

    #existing_patient_info -> pydantic object -> updated bmi + verdict
    existing_patient_info['id']=patient_id
    patient_pydantic_odj = Patient(**existing_patient_info)

    #-> pydantic obj ->dict

    existing_patient_info = patient_pydantic_odj.model_dump(exclude = 'id')

    #add this dict to data
    data[patient_id] = existing_patient_info

    #Save Data
    save_data(data)

    return JSONResponse(status_code=200,content={'message':'Patient Updated'})



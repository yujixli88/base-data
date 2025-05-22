from fastapi import FastAPI, Form
from pydantic import BaseModel
from typing import Optional

app = FastAPI()

class UserInput(BaseModel):
    name: str
    email: str
    password: str

@app.get("/")
async def root():
    return {
        "message": "Welcome to the user registration API"
    }

@app.post("/register")
async def register(
    name: str = Form(...),
    email: str = Form(...),
    password: str = Form(...)
):
    user_input = UserInput(
        name=name,
        email=email,
        password=password
    )
    # Here you would typically save to database
    return {"message": "User registered successfully", "user": user_input}

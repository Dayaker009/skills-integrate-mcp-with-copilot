# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

   ## Authentication (development/demo)

   This project includes a simple in-memory authentication demo used for the exercise.

   - Login: `POST /auth/login` with JSON `{ "email": "...", "password": "..." }` returns a `token`.
   - Register: `POST /auth/register` with JSON `{ "email": "...", "password": "..." }` (optional `role` query param, default `student`).

   Use the token with an `Authorization: Bearer <token>` header when calling protected endpoints such as signing up for activities.

   Example login (curl):

   ```bash
   curl -X POST -H "Content-Type: application/json" \
      -d '{"email":"student@mergington.edu","password":"studentpass"}' \
      http://localhost:8000/auth/login
   ```


## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.

# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teacher login to sign up or unregister students

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Set the teacher credentials in the environment. For example, in a shell:

   ```
   export TEACHER_USERNAME=teacher
   export TEACHER_PASSWORD='use-a-unique-secret'
   ```

   Do not commit credentials to the repository. Use HTTPS when exposing the app
   beyond a trusted local development environment.

3. Run the application from the repository root:

   ```
   uvicorn src.app:app --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                     | Validate teacher credentials using HTTP Basic authentication        |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (teacher authentication required)                 |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)              |

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

All activity data is stored in memory, which means it resets when the server
restarts. Teacher credentials are configured with `TEACHER_USERNAME` and
`TEACHER_PASSWORD`; protected endpoints return an error if they are unset.

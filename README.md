
# Secure NetPulse Devices API

## 1. Project Overview

The Secure NetPulse Devices API is a REST API built using
FastAPI.

It allows users to view network device information publicly
and protects device modification operations using JWT
authentication.

## 2. Technologies Used

- Python
- FastAPI
- Uvicorn
- Pydantic
- PyJWT
- pwdlib
- Argon2 password hashing
- HTTPX

## 3. Project Structure

```text
netpulse-devices-api/
│
├── main.py
├── requirements.txt
├── README.md
├── .gitignore
└── evidence/
```

## 4. Device Information

Each device contains:

- id
- name
- device_type
- status
- location

The application uses in-memory storage.
No database is required.

## 5. API Endpoints

| Method | Endpoint | Access |
|---|---|---|
| POST | /auth/token | Public |
| GET | /devices | Public |
| GET | /devices/{device_id} | Public |
| POST | /devices | Protected |
| PUT | /devices/{device_id} | Protected |
| PATCH | /devices/{device_id} | Protected |
| DELETE | /devices/{device_id} | Protected |

## 6. Installation

Create a virtual environment:

```powershell
python -m venv .venv
```

Activate it in Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

## 7. Configure Environment Variables

Set the training credentials and JWT signing secret
in your PowerShell terminal:

```powershell
$env:DEMO_USERNAME="netpulseuser"
$env:DEMO_PASSWORD="ChooseYourOwnStrongPassword"
$env:JWT_SECRET="ReplaceWithYourOwnLongRandomSecret"
```

Use your own training values.
Do not commit real credentials or JWT secrets to GitHub.

## 8. Run the Application

Start the FastAPI server:

```powershell
python -m uvicorn main:app --reload
```

Open Swagger documentation:

http://127.0.0.1:8000/docs

## 9. Authentication

1. Open the /auth/token endpoint.
2. Enter the configured username and password.
3. Execute the request.
4. Copy the access token without sharing it.
5. Click the Authorize button in Swagger.
6. Enter the username and password in the OAuth2 form.
7. Authorize the API.
8. Test the protected POST, PUT, PATCH and DELETE endpoints.

## 10. Security Features

- Passwords are hashed before being retained in the app.
- JWT tokens use HS256 signing.
- JWT expiry is validated.
- JWT subject must match the configured training username.
- Protected write operations require a valid Bearer token.
- Credentials and signing secrets are read from environment variables.

## 11. Testing Checklist

- Public GET /devices returns HTTP 200.
- Existing device returns HTTP 200.
- Missing device returns HTTP 404.
- Missing bearer token is rejected with HTTP 401.
- Invalid bearer token is rejected with HTTP 401.
- Invalid login is rejected with HTTP 401.
- Valid login returns HTTP 200.
- Authenticated POST returns HTTP 201.
- Authenticated PUT returns HTTP 200.
- Authenticated PATCH returns HTTP 200.
- Authenticated DELETE returns HTTP 204.
- Deleted device returns HTTP 404.

Verify the API using both Swagger and Postman.

## 12. Important Notes

- Device information is stored in memory.
- Restarting the server resets the initial device data.
- GET endpoints are public.
- All device-changing endpoints require authentication.
- Never share a valid JWT token in screenshots.
- Use HTTPS before exposing bearer-token authentication
  outside the local training environment.

# Employee application

* Language: Python 3
* Framework: Flask
* Web application
* VCS: GitHub

Employee has an ID and a name.

This application has a HTML UI and a REST API.

Use mySQL.

DEMO.

demo2-2.

services:
  postgres:
    image: postgres
    environment:
      POSTGRES_DB: employees
      POSTGRES_USERS: employees
      POSTGRES_PASSWORD: employees
    healthcheck:
      test: ["CMD_SHELL", "sh -c 'pg_isready -U employees -d employees'"]
  employees-python:
    image: employyes-python
    depends_on:
      postgres:
        condition: service_healthy
    ports:
      - "81:5000"
    environment:
      DATABASE_HOST: postgres
    healthcheck:
      test: curl --fail http://localhost:5000 | exit 1
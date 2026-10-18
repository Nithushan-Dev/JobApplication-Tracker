# Job Application Tracker

A Spring Boot REST API for managing and tracking job applications with CRUD operations, filtering, pagination, validation, global exception handling, JWT authentication, and Docker support.

## 🎯 Project Overview

Job Application Tracker is a backend application built with Java and Spring Boot to manage job application records through RESTful APIs.

This project demonstrates practical backend development concepts, including layered architecture, DTOs, database persistence, validation, API documentation, authentication, authorization, and containerization.

## 🛠️ Tech Stack

- **Language:** Java 21
- **Framework:** Spring Boot
- **Security:** Spring Security
- **Authentication:** JWT
- **Password Hashing:** BCrypt
- **Persistence:** Spring Data JPA / Hibernate
- **Database:** MySQL
- **Build Tool:** Maven
- **API Documentation:** Swagger UI / OpenAPI
- **Containerization:** Docker and Docker Compose
- **Version Control:** Git and GitHub

## ✨ Features

### Job Application Management

- Create, retrieve, update, and delete job applications
- Retrieve applications by ID
- Filter by company, status, and location
- Combine multiple filtering criteria
- Pagination support

### Validation and Error Handling

- Request validation using DTOs
- Global exception handling
- Meaningful validation error responses
- Appropriate HTTP status codes
- Consistent REST API error responses

### Authentication and Security

- User registration and login
- BCrypt password hashing
- JWT generation, validation, and expiration
- Stateless authentication
- Role information in JWTs
- Protected application endpoints
- Bearer token authentication in Swagger UI
- Environment-based JWT secret configuration

### Docker Support

- Dockerfile for the Spring Boot application
- Docker Compose configuration for the application and MySQL
- Environment-based configuration for credentials and secrets

## 🏗️ Application Architecture

The project follows a layered architecture:

```text
Client
  |
  v
Controller
  |
  v
Service
  |
  v
Repository
  |
  v
MySQL Database
```

### Main Components

- **Controller Layer:** Handles HTTP requests and API endpoints.
- **Service Layer:** Contains application and business logic.
- **Repository Layer:** Performs database operations using Spring Data JPA.
- **DTOs:** Define API request and response structures.
- **Security Configuration:** Defines authentication and authorization rules.
- **JwtService:** Handles JWT generation and token information.
- **JwtFilter:** Processes JWT authentication for protected requests.
- **CustomUserDetailsService:** Loads user details for Spring Security.
- **PasswordEncoder:** Uses BCrypt to hash and verify passwords.
- **Exception Handling:** Provides consistent error responses.

## 🔐 Authentication Flow

### User Registration

```text
POST /auth/register
        |
        v
AuthController
        |
        v
AuthService
        |
        v
BCrypt PasswordEncoder
        |
        v
UserRepository
        |
        v
MySQL
```

Passwords are hashed using BCrypt before being stored. The registration response does not expose the stored password hash.

### User Login

```text
POST /auth/login
        |
        v
AuthenticationManager
        |
        v
DaoAuthenticationProvider
        |
        v
CustomUserDetailsService
        |
        v
Password Verification
        |
        v
JWT Generation
        |
        v
Authentication Response
```

### Protected Requests

The client sends the token in the request header:

```text
Authorization: Bearer <JWT>
```

The JWT filter validates the token and establishes the authenticated security context before the request reaches a protected endpoint.

## 🔌 API Endpoints

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/register` | Register a new user |
| POST | `/auth/login` | Authenticate a user and generate a JWT |

### Job Applications

| Method | Endpoint | Description |
|---|---|---|
| GET | `/applications` | Retrieve applications with optional filtering |
| GET | `/applications/{id}` | Retrieve an application by ID |
| POST | `/applications` | Create an application |
| PUT | `/applications/{id}` | Update an application |
| DELETE | `/applications/{id}` | Delete an application |
| GET | `/applications/page` | Retrieve applications with pagination |

**Note:** Job application endpoints require a valid JWT.

## 🔎 Filtering and Pagination

Applications can be filtered by:

- Company
- Application status
- Location
- Multiple filtering criteria

Pagination is available when retrieving application records.

## 📖 API Documentation

The API is documented using Swagger UI and OpenAPI.

- **Swagger UI:** http://localhost:8080/swagger-ui/index.html
- **OpenAPI specification:** http://localhost:8080/v3/api-docs

Use the Swagger UI **Authorize** option to provide a valid Bearer JWT before testing protected endpoints.

These URLs work when the application is running locally.

## 🗄️ Database

The application uses MySQL for persistent storage and Spring Data JPA / Hibernate for database interaction.

The database stores:

- User information
- Job application records

Passwords are stored as BCrypt hashes rather than plain-text passwords.

## 🐳 Run with Docker Compose

### Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Git

### 1. Clone the repository

```bash
git clone https://github.com/Nithushan-Dev/JobApplication-Tracker.git
cd JobApplication-Tracker
```

### 2. Configure environment variables

Create a `.env` file in the project root, alongside `docker-compose.yml`.

Add values matching your Docker Compose configuration:

```dotenv
DB_USERNAME=jobuser
DB_PASSWORD=your_database_password
JWT_SECRET=your_long_random_secret
```

Replace the example values with your local credentials. The database username and password must match the MySQL configuration in `docker-compose.yml`.

**Important:** Keep `.env` private and ensure it is excluded by `.gitignore`. Never commit actual credentials or JWT secrets.

### 3. Build the application

```bash
./mvnw clean package -DskipTests
```

### 4. Start the services

Make sure Docker Desktop is running, then execute:

```bash
docker compose up -d --build
```

Docker Compose builds the application image and starts the application and MySQL services.

### 5. Access Swagger UI

Open:

http://localhost:8080/swagger-ui/index.html

Register a user, log in, obtain a JWT, and use the Authorize option to test protected endpoints.

### Useful Docker commands

Check running containers:

```bash
docker compose ps
```

View application logs:

```bash
docker compose logs -f app
```

View database logs:

```bash
docker compose logs -f db
```

Stop the services:

```bash
docker compose down
```

Start the services again:

```bash
docker compose up -d
```

**Database note:** Configure persistent MySQL storage using a named volume if you want your data to survive container removal.

## ▶️ Run Locally Without Docker

### Prerequisites

- Java 21
- MySQL
- Maven or the included Maven Wrapper

### 1. Configure MySQL

Create the `jobtracker` database and configure the application to connect to it.

### 2. Configure environment variables

Set these variables in your local environment:

```text
DB_USERNAME
DB_PASSWORD
JWT_SECRET
```

Ensure `application.properties` references the variables rather than containing real secrets.

### 3. Start the application

On macOS or Linux:

```bash
./mvnw spring-boot:run
```

On Windows:

```bat
mvnw.cmd spring-boot:run
```

The application runs at:

http://localhost:8080

## 🧠 What I Learned

- Java and Spring Boot
- REST API design
- Controller-Service-Repository architecture
- DTOs and request validation
- Spring Data JPA and MySQL integration
- CRUD operations, filtering, and pagination
- Global exception handling
- Swagger and OpenAPI documentation
- Spring Security authentication and authorization
- BCrypt password hashing
- `UserDetailsService`
- `DaoAuthenticationProvider`
- `AuthenticationManager`
- JWT generation, validation, and expiration
- JWT filters and security context
- Stateless authentication
- Environment-based secret management
- Docker and Docker Compose
- Git and GitHub workflow

## 🚀 Future Improvements

- Expand automated test coverage
- Improve role-based authorization
- Add OAuth2 login with Google or GitHub
- Build a frontend for the API
- Deploy the application to the cloud
- Improve container startup reliability and database persistence
- Explore additional backend technologies


## Screenshots

### Swagger UI

Interactive API documentation and testing interface.

![Swagger UI](screenshots/swagger-overview.png)

### Get Applications with Filtering

![GET Applications](screenshots/get-applications.png)

### Create Application

![POST Application](screenshots/post-application.png)

### Update Application

![PUT Application](screenshots/put-application.png)




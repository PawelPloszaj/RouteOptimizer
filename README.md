# 🗺️ Route Optimizer

A web application for optimizing travel routes by reordering waypoints efficiently. It consists of a Spring Boot backend and an Angular frontend. The application uses free and open external APIs to calculate distances and generate optimized routes.

---

## 🛠 Technology Stack

- **Backend**: Java 17, Spring Boot, Maven
- **Frontend**: Angular 17+
- **Database**: MySQL
- **Other**: Docker, Docker Compose
- **Security (Planned)**: JWT, CORS, user authentication

---

## 🧑‍💻 Running Locally with Docker

1. **Run the application:**

```bash
docker-compose up --build
```

2. **Access the app:**
- Frontend (Angular, served via NGINX): http://localhost:4200
- Backend (Spring Boot): http://localhost:8080

---

## 📁 Project Structure

```
RouteOptimizer/
├── backend/                 # Spring Boot application
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── frontend/                # Angular application
│   ├── src/
│   ├── angular.json
│   └── Dockerfile
├── docker-compose.yml       # Combined Docker configuration
└── README.md
```

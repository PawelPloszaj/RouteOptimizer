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

## 📥 One-time Setup Instructions (OSM & ORS Initialization)

### 🗺️ Map Data (OSM)

This project uses OpenStreetMap data to build routing graphs with OpenRouteService.

### 1. Downloading OSM data

You need to manually download the desired `.osm.pbf` file (e.g., for Poland):

- **Poland extract:** [https://download.geofabrik.de/europe/poland-latest.osm.pbf](https://download.geofabrik.de/europe/poland-latest.osm.pbf)
- More countries and regions: [https://download.geofabrik.de/](https://download.geofabrik.de/)

Place the downloaded file in the following location:

```
ors/data/osm_file.pbf
```

> ⚠️ This file is not included in the repository due to its large size (~1.8 GB).


### 2. Modify `docker-compose.yml` for First Run Only

Before running the application for the first time, apply these changes:

- In the `ors` service, set:
  ```yaml
  environment:
    - BUILD_GRAPHS=True
  ```

- In the `nominatim` service, **remove**:
  ```yaml
  - NOMINATIM_MODE=frontend
  ```

This will trigger the full import of OSM data into both Nominatim and ORS.

### 3. Run the Application

```bash
docker-compose up --build
```

Wait until import is fully completed — this can take 15–45+ minutes depending on hardware.

### 4. Restore `docker-compose.yml` for Subsequent Runs

After import is done, to speed up next startups:

- Change `BUILD_GRAPHS=False` in the `ors` service.
- Restore `NOMINATIM_MODE=frontend` in the `nominatim` service.

---

## 🧑‍💻 Running Locally with Docker

1. **Run the application:**

```bash
docker-compose up --build
```

2. **Access the app:**
- Frontend (Angular, served via NGINX): http://localhost:4200
- Backend (Spring Boot): http://localhost:8080
- OpenRouteService API: http://localhost:8081
- Nominatim API: http://localhost:7070

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
├── ors/                     # OpenRouteService folder
│   ├── ors-conf/            # ORS app config
│   │   └── ors-config.json
│   ├── data/                # OSM data folder (ignored by Git)
│   │   └── osm_file.pbf
├── docker-compose.yml       # Combined Docker configuration
└── README.md
```

---

## 📝 Notes

- `ors/data` is excluded from Git using `.gitignore`, as the OSM `.pbf` file is ~1.8 GB.
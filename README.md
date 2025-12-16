# ErrorsTracer Docker Setup

This repository contains the **Docker Compose setup** to run the ErrorsTracer project, including the backend, frontend (dashboard), and PostgreSQL database. Follow the steps below to set up and run the project locally.

---

## 📌 Prerequisites

Make sure you have **Docker** installed on your machine.  
Install Docker from the official website: [https://www.docker.com/get-started](https://www.docker.com/get-started)

---

## 🛠 Project Setup

### Step 1: Clone Repositories

Clone the following repositories from the **ErrorsTracer organization**:

```bash
git clone https://github.com/errorstracer/backend
git clone https://github.com/errorstracer/dashboard
git clone https://github.com/errorstracer/docker-compose
```

### Step 2: Organize Project Structure

Place all three repositories in **one folder** to keep the project organized:

```
project-root/
	├── backend/
	├── dashboard/
	└── docker-compose/
```

### Step 3: Setup The Backend

- Navigate to the backend folder:

```bash
cd backend
```

- Add your `.env` file with all required environment variables.
- Build the Docker image:

```bash
docker build -t errors-tracer-backend .
```

### Step 4: Setup Dashboard (Frontend)

- Navigate to the dashboard folder:

```bash
cd dashboard
```

- Add your `.env` file with all required environment variables.
- Build the Docker image:

```bash
docker build -t errors-tracer-dashboard .
```

### Step 5: Setup PostgreSQL

- Pull the official Postgres image:

```bash
docker pull postgres
```

- Run the Postgres container (if not already running via compose):

```bash
docker run --name database -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -v postgres_data:/var/lib/postgresql/data -d postgres
```

- Login to Postgres and create your database:

```bash
docker exec -it database psql -U postgres
CREATE DATABASE your_database_name;
```

### Step 6: Run Docker Compose

- Navigate to the `docker-compose` folder:

```bash
cd docker-compose
```

- Start all services (backend, frontend, and database):

```bash
docker compose up -d
```

## 🔗 Project Architecture

```
+----------------+       +----------------+       +----------------+
|  Dashboard     |  -->  |  Backend API   |  -->  |  PostgreSQL DB |
|  (Next.js)     |       |  (NestJS)      |       |  (Postgres)    |
+----------------+       +----------------+       +----------------+
```

- **Frontend (Dashboard)** communicates with **Backend API**
- **Backend API** communicates with **PostgreSQL database**
- All services are orchestrated using **Docker Compose**.

## 🌐 Default Ports

```
## 🌐 Default Ports

| Service    | Container Port | Notes                                  |
|------------|----------------|----------------------------------------|
| Frontend   | 3000           | Accessible via browser locally         |
| Backend    | 4973           | API requests from frontend             |
| PostgreSQL | 5431           | Connect using Sequelize ORM            |
```

> Adjust ports if needed in your `.env` or `docker-compose.yml`.

## ✅ Project is Ready

Once the services are up, you can access:

- **Frontend (Dashboard)**: via your browser if running locally, or via Nginx on the server.
- **Backend API**: using the exposed ports defined in the Docker Compose file.
- **PostgreSQL**: accessible via the database container.

---

## ⚡ Notes

- Make sure `.env` files are correctly configured before building images.
- Use `docker compose down` to stop and remove containers when done.
- Use `docker logs <container_name>` to debug issues.

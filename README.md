## Running the Project with Docker

This project provides a full-stack JavaScript application with separate backend and frontend services, orchestrated via Docker Compose. The setup uses Node.js v22.13.1 for both backend and frontend builds, and Nginx to serve the frontend. Redis is included as a service dependency for the backend.

### Requirements
- Docker and Docker Compose installed
- No local Node.js or Nginx installation required

### Environment Variables
- Backend: Copy `backend/.env.example` to `backend/.env` and fill in required values before running (see comments in the example file).
- Frontend: Copy `frontend/.env.example` to `frontend/.env` if you need to override defaults.

### Build and Run
1. Ensure your `.env` files are in place as described above.
2. From the project root, run:

   ```sh
   docker compose up --build
   ```

   This will build and start all services.

### Service Ports
- **Backend API:** http://localhost:3000
- **Frontend (Nginx):** http://localhost:80
- **Redis:** localhost:6379 (for development/debugging)

### Special Configuration
- The backend and frontend Dockerfiles use Node.js version `22.13.1-slim` for builds.
- The backend runs as a non-root user for improved security.
- The frontend is built with Vite and served by Nginx using a custom `nginx.conf`.
- Redis is required and started automatically by Docker Compose.

> **Note:**
> - If you need persistent storage for uploads or logs, add Docker volumes to the `docker-compose.yml` as needed.
> - Healthchecks are configured for Redis to ensure service readiness.

For more details on project structure or advanced usage, refer to the other documentation files in the repository.
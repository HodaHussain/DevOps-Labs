
# Lab 8: Containerized Node.js and MySQL Stack Using Docker Compose

## Objective
Deploy a Node.js web application and a MySQL database using Docker Compose.

## Technologies Used
- Docker
- Docker Compose
- Node.js
- Express.js
- MySQL 8.0
- Docker Volumes and Networks
- Docker Hub

## Project Structure
```text
Lab8/
├── Dockerfile
├── docker-compose.yml
├── package.json
├── server.js
├── db.js
└── frontend/
    ├── index.html
    └── assets/
        └── ivolve-logo.png
```

## Services
### Application
- Image: `hodahuss22/ivolve-app:latest`
- Port: `3000:3000`
- Database host: `db`
- Logs directory: `/app/logs`

### MySQL Database
- Image: `mysql:8.0`
- Database: `ivolve`
- Persistent storage: `db_data`
- Health check configured.

## Docker Resources
- Network: `ivolve-net`
- Database volume: `db_data`
- Application logs volume: `app_logs`

## Deployment
Build and start the services:

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker ps
```

Check application readiness:

```bash
curl -i http://localhost:3000/ready
```

Check application logs:

```bash
docker exec ivolve-app cat /app/logs/access.log
```

## Docker Hub
Docker Hub image: [hodahuss22/ivolve-app](https://hub.docker.com/r/hodahuss22/ivolve-app)

## Result
The application and MySQL database were started successfully using Docker Compose. The readiness endpoint returned HTTP 200 OK, and application access logs were generated.

Persistent volumes were configured for database data and application logs.
<img width="1198" height="445" alt="Lab8{1}" src="https://github.com/user-attachments/assets/c331294f-ae6d-4e4f-9f70-c1e1fa4b8f1d" />
<img width="1816" height="822" alt="Lab8{5}" src="https://github.com/user-attachments/assets/1f7d22c6-31a5-45da-aeb1-ee218515d467" />
<img width="1847" height="931" alt="Lab8{4}" src="https://github.com/user-attachments/assets/4bfacfdd-0468-465d-8123-e0ce72bc601d" />
<img width="1182" height="442" alt="Lab8{3}" src="https://github.com/user-attachments/assets/db6d4713-f2cb-4168-b1f6-9190851102d3" />
<img width="1180" height="256" alt="Lab8{2}" src="https://github.com/user-attachments/assets/3a52d2f8-f543-47bc-a093-3f8bfff41cd3" />

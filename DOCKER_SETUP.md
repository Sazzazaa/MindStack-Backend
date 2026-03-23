# Docker Setup Guide for Backend

This guide explains how to run the NestJS backend with Docker and Docker Compose.

## Prerequisites

- Docker Desktop installed
- Docker Compose available (`docker compose`)
- Git

## Project Layout

Run compose from the project root where `docker-compose.yml` exists:

```bash
Mayfare/
  docker-compose.yml
  MindStack-Backend/
```

## Quick Start (Recommended)

```bash
# From project root (Mayfare)
docker compose up --build
```

This will:
- Build the backend image from `MindStack-Backend/Dockerfile`
- Start MongoDB with authentication
- Start backend on `http://localhost:3000`
- Mount `MindStack-Backend/src/` for live reload

## Environment Variables

The backend service loads values from:
- `MindStack-Backend/.env` via `env_file`

Compose also supports these optional variables (with defaults) from your shell or root `.env` file:
- `MONGO_INITDB_ROOT_USERNAME` (default: `admin`)
- `MONGO_INITDB_ROOT_PASSWORD` (default: `password`)

If you want custom Mongo credentials, set both before startup and keep backend URI in sync.

Example PowerShell session:

```powershell
$env:MONGO_INITDB_ROOT_USERNAME = "admin"
$env:MONGO_INITDB_ROOT_PASSWORD = "strong-password"
docker compose up --build
```

## Common Commands

```bash
# Start in background
docker compose up -d --build

# View service status
docker compose ps

# View logs
docker compose logs -f backend
docker compose logs -f mongodb

# Stop services
docker compose down

# Stop and remove volume (clean Mongo data)
docker compose down -v

# Shell into backend container
docker compose exec backend sh

# Run seed scripts
docker compose exec backend npm run seed
docker compose exec backend npm run seed:simple
docker compose exec backend npm run seed:clean
```

## Manual Image Run (Without Compose)

```bash
# From project root
cd MindStack-Backend

docker build -t mindstack-backend:latest .

docker run -p 3000:3000 \
  -e NODE_ENV=production \
  -e MONGODB_URI=mongodb://localhost:27017/dacn \
  mindstack-backend:latest
```

## MongoDB Access

```bash
# Connect to Mongo inside compose network
docker compose exec mongodb mongosh -u admin -p password --authenticationDatabase admin

# Connect from host
mongosh "mongodb://admin:password@localhost:27017/dacn?authSource=admin"
```

## Troubleshooting

### Port 3000 already in use

```powershell
netstat -ano | findstr :3000
```

Then stop the conflicting process, or change compose port mapping.

### Backend cannot connect to MongoDB

```bash
docker compose ps
docker compose logs mongodb
docker compose logs backend
```

Check:
- `mongodb` is `healthy`
- backend uses `mongodb` hostname (not `localhost`) in container URI
- Mongo credentials match between services

### Hot reload not working

Check that `MindStack-Backend/src/` is mounted and backend is running `npm run start:dev`.

```bash
docker compose logs -f backend
```

Look for watch mode output from NestJS.

## Security Notes

- Do not commit real secrets to any `.env` file.
- Use strong Mongo credentials outside local development.
- Restrict CORS and API keys before production deployment.
- Prefer secret managers for cloud environments.

## Further Reading

- Docker docs: https://docs.docker.com/
- NestJS deployment: https://docs.nestjs.com/deployment
- MongoDB image: https://hub.docker.com/_/mongo

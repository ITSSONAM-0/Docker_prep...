# 1. What is Docker?
Docker is a platform used to build, ship, and run applications inside containers.
- Containers are lightweight.
- Containers include everything the application needs.
- Containers run the same on any machine (Windows/Mac/Linux/server).

# 2. Why Docker is Used
- Same environment for all developers.
- Faster deployment.
- Lightweight compared to Virtual Machines.
- Easy to scale.
- Supports microservices architecture.

# 3. Docker Terminology
# Image
A read-only template used to create containers.
Example:
node:18, python:3.10, mysql, nginx

# Container
A running instance of an image.

# Dockerfile
A file containing instructions to build a Docker image.

# Docker Hub
Public cloud registry where Docker images are stored.

# 4. Install Check
```nginx
docker --version
docker info
```

# 5. Basic Docker Commands
Images
```arduino
docker pull <image-name>
docker images
docker rmi <image-name>
```

# Containers
```
docker run <image-name>
docker run -d <image-name>
docker run -p 8080:80 <image-name>
docker ps
docker ps -a
docker stop <container-id>
docker rm <container-id>
```
# Logs
```
docker logs -f <container-id>
```
# Access inside container
```
docker exec -it <container-id> bash
```
# 6. Dockerfile — Example

Create a file named Dockerfile:
```
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```
# Build Image:
```
docker build -t myapp .
```
# Run Container:
```
docker run -p 3000:3000 myapp
```
# 7. Docker Volumes
Used to store data permanently.
Example:
```
docker run -d -v mydata:/var/lib/mysql mysql
```
# 8. Docker Networks
Create network:
```
docker network create mynetwork
```

# Run containers inside same network:
```
docker run -d --network=mynetwork --name=api myapi
docker run -d --network=mynetwork --name=db mongo
```
# 9. Docker Compose
docker-compose.yml Example
```
version: "3"
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    restart: always
    ports:
      - "27017:27017"
```
# Start
```
docker compose up -d
```
# Stop
```
docker compose down
```
# 10. Full Project Using Docker
Node.js + MongoDB
Folder structure:
```
project/
  backend/
    Dockerfile
    package.json
    index.js
  docker-compose.yml
```
# Backend Dockerfile:
```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "index.js"]
```
# docker-compose.yml:
```
version: "3"
services:
  api:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    ports:
      - "27017:27017"
```

# Run:
```
docker compose up -d
```
# 11. Docker Interview Questions (With Answers)

# Q1. What is Docker?
A container platform used to run applications in isolated environments.

# Q2. What is the difference between Image and Container?
Image = Blueprint
Container = Image’s running instance

# Q3. What is Dockerfile?
A text file with instructions to create a Docker image.

# Q4. What is Docker Compose?
Tool to run multiple containers at once.

# Q5. What are Docker volumes?
Storage used to persist data.

# 12. Docker Learning Roadmap
1. Docker Basics
2. Images & Containers
3. Dockerfile
4. Volumes
5. Networks
6. Docker Compose
7. Deployment
8. Kubernetes (Advanced)

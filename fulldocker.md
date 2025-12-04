# 1. Why do we need Docker?
- To ensure consistent environments across all machines
- Eliminates “works on my machine” problems
- Lightweight, fast, and easy to deploy
- Helps isolate applications
- Makes development, testing, and production environments identical
- Enables scalable microservice architecture

# 2. What is Docker? (Container and Image)
Docker is a containerization platform used to package applications and their dependencies.

# ocker Image
- A read-only template
- Contains app code + dependencies
- Example: node:18, nginx, mongo

# Docker Container
- A running instance of an image
- Lightweight and isolated environment

# 3. Docker Installation
- Install Docker Desktop for Windows/Mac
- For Linux:
```
sudo apt update
sudo apt install docker.io
```
# Verify installation:
```
docker --version
docker info
```
# 4. Important Docker Commands
```
docker pull <image>
docker run <image>
docker ps
docker ps -a
docker stop <container_id>
docker rm <container_id>
docker rmi <image_name>
docker exec -it <container_id> bash
docker logs <container_id>
```
# 5. Docker vs Virtual Machine
| Docker                 | Virtual Machine            |
| ---------------------- | -------------------------- |
| Lightweight            | Heavy                      |
| Starts in seconds      | Starts in minutes          |
| Shares host OS kernel  | Has full guest OS          |
| Low resource usage     | High resource usage        |
| Best for microservices | Best for full OS isolation |

# 6. Image vs Container
- Image: Blueprint/template
- Container: Image in running state

# 7. More Docker Commands
```
docker start <id>
docker restart <id>
docker inspect <id>
docker top <id>
docker stats
docker history <image>
docker system prune
```
# 8. Port Binding
Port mapping exposes container port to your system.

Format:
```
host_port:container_port
```
# Example:
```
docker run -p 8080:80 nginx
```
# 9. Troubleshoot Commands
```
docker logs <id>
docker inspect <id>
docker stats
docker events
docker system df
docker system prune
```
# 10. Use Case: Using Docker for Development
- Run FE, BE, and DB in separate containers
- No need to install databases locally
- Same environment across all developers
- Easy to reset, update, or upgrade environments

# 11. Docker Network
 Create network:
 ```
docker network create mynetwork
```
# Run inside network:
```
docker run -d --network=mynetwork --name=db mongo
docker run -d --network=mynetwork --name=nodeapp nodeapp
```
# 12. Set up Mongo and Mongo Express
MongoDB
```
docker run -d --name mongo -p 27017:27017 mongo
```
# Mongo Express
```
docker run -d --name mongo-express -p 8081:8081 \
-e ME_CONFIG_MONGODB_SERVER=mongo \
--network=mynetwork mongo-express
```
# 13. Connect DB with Node App
Use container name instead of localhost:
```
mongodb://mongo:27017/mydb
```
# Node.js example:
```
mongoose.connect("mongodb://mongo:27017/mydb")
```
# 14. Docker Compose
docker-compose.yml
```
version: "3"
services:
  mongo:
    image: mongo
    ports:
      - "27017:27017"

  mongo-express:
    image: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_SERVER: mongo

  nodeapp:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongo
```
# Run:
```
docker compose up -d
```
# Stop:
```
docker compose down
```
# ⭐ 15. Use Case: Dockerizing Our App
- Dockerizing an application means:
- Packaging it inside a container
- Ensuring it runs the same everywhere
- No dependency issues
- Easy to deploy on any server
- Example: Convert a Node, Python, or Java app into a Docker image.

# ⭐ 16. Creating a Dockerfile
Example Dockerfile (Node app):
```
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```
# Build image:
```
docker build -t myapp .
```
# Run:
```
docker run -p 3000:3000 myapp
```
# ⭐ 17. Publish Image on DockerHub
Step 1: Login
```
docker login
```
# Step 2: Tag image
```
docker tag myapp username/myapp:v1
```
# Step 3: Push image
```
docker push username/myapp:v1
```
# ⭐ 18. Docker Volumes
- Volumes store persistent data.
- Use cases:
- Database data
- File uploads
- Caches

# Run with volume:
```
docker run -v myvolume:/data db-image
```
# ⭐ 19. Volume Commands
```
docker volume create myvolume
docker volume ls
docker volume inspect myvolume
docker volume rm myvolume
```
# ⭐ 20. Revisiting Docker Network
- Docker networks allow containers to communicate internally.
- Types:
     - bridge (default)
     - host
     - overlay

Commands:
```
docker network ls
docker network create mynetwork
docker network inspect mynetwork
docker network rm mynetwork
```
#Good luck....

🐳 Day 59 – Advanced Docker
🎯 Objective
Learn advanced Docker concepts focused on security, optimization, resource management, monitoring, and production-ready container practices.
🔐 1. Docker Security Best Practices
Docker containers should be designed with security in mind.
Important practices:
Use trusted base images.
Keep images updated.
Run containers as non-root users.
Don't store secrets inside images.
Use .dockerignore.
Scan images for vulnerabilities.
Follow least privilege.
Remove unnecessary packages.
Limit container resources.
Use read-only filesystems where appropriate.
👤 2. Run Containers as Non-Root User
Running applications as root inside containers can increase the impact of a container compromise.
Example Dockerfile:
FROM node:18-alpine

WORKDIR /app

RUN addgroup -S appgroup && \
    adduser -S appuser -G appgroup

COPY . .

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 3000

CMD ["node", "server.js"]
Check the user:
docker exec <container> whoami
Expected:
appuser
🚫 3. .dockerignore
.dockerignore prevents unnecessary files from being included in the Docker build context.
Example:
node_modules
.git
.gitignore
*.log
.env
coverage
dist
README.md
Benefits
Smaller build context
Faster builds
Less unnecessary data
Reduced risk of accidentally including sensitive files
🏗️ 4. Multi-Stage Builds
Multi-stage builds separate the build environment from the final runtime environment.
Example:
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build


FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist

EXPOSE 3000

CMD ["node", "dist/server.js"]
Architecture
Build Stage
     │
     ▼
Compile / Build
     │
     ▼
Production Stage
     │
     ▼
Small Final Image
Benefits
Smaller images
Fewer unnecessary dependencies
Faster deployment
Reduced attack surface
Cleaner production images

❤️ 5. Docker Healthcheck
A health check allows Docker to determine whether a container's application is responding correctly.
Example:
HEALTHCHECK --interval=30s \
            --timeout=10s \
            --retries=3 \
            CMD wget -qO- http://localhost:3000/health || exit 1
Check container health:
docker ps
Example:
STATUS
Up 2 minutes (healthy)
Possible states:
Starting
Healthy
Unhealthy
📊 6. Resource Limits
Containers can consume excessive CPU or memory if they are not controlled.
Example:
docker run -d \
  --name myapp \
  --cpus="1.5" \
  --memory="512m" \
  myapp:1.0
This limits the container to approximately:
CPU    → 1.5 CPUs
Memory → 512 MB
Check resource usage:
docker stats

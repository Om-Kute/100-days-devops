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

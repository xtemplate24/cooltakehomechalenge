# Build stage — compiles the React app to static files
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Serve stage — uses the moving stable-alpine tracking tag to get latest updates
FROM nginxinc/nginx-unprivileged:stable-alpine

# Temporarily switch to root to perform security package upgrades
USER root

# Pull latest security patches to fix libexpat and resolve Trivy build blocks
RUN apk update && apk upgrade libexpat

# Revert immediately to the unprivileged application user
USER 101

# Copy the static web build artifacts into place
COPY --chown=101:101 --from=build /app/dist /usr/share/nginx/html

EXPOSE 8080
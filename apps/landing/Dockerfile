# Build stage — compiles the React app to static files
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Serve stage — same pinned base as the other apps, unprivileged, no Node at runtime
FROM nginxinc/nginx-unprivileged:stable-alpine@sha256:daa17b944bac2b578e962da4c61ad72a59233b3c63abea17113acaf4e6b9aea4
COPY --chown=101:101 --from=build /app/dist /usr/share/nginx/html
USER 101
EXPOSE 8080

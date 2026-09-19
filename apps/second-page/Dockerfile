FROM nginxinc/nginx-unprivileged:stable-alpine@sha256:daa17b944bac2b578e962da4c61ad72a59233b3c63abea17113acaf4e6b9aea4
COPY --chown=101:101 index.html /usr/share/nginx/html/index.html
USER 101
EXPOSE 8080

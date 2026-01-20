# syntax=docker/dockerfile:1

# Build Stage
FROM node:lts-alpine AS build
WORKDIR /bookcars/admin

# Copy source
COPY ./admin ./ 
COPY ./packages /bookcars/packages

# Install & build
RUN npm install --force
# Use env var injected by Dokploy for API URL at build time if needed
# Example: ARG REACT_APP_API_BASE_URL
# ENV REACT_APP_API_BASE_URL=${REACT_APP_API_BASE_URL}
RUN npm run build

# Production Stage
FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf -- *
COPY --from=build /bookcars/admin/build .
COPY ./admin/nginx.conf /etc/nginx/conf.d/default.conf

# Expose standard HTTP port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

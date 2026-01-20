# syntax=docker/dockerfile:1

# Build Stage
FROM node:lts-alpine AS build
WORKDIR /bookcars/frontend

# Copy source
COPY ./frontend ./ 
COPY ./packages /bookcars/packages

# Install dependencies & build
RUN npm install --force

# Build-time environment variable (for React API URL)
ARG REACT_APP_API_BASE_URL
ENV REACT_APP_API_BASE_URL=${REACT_APP_API_BASE_URL}

RUN npm run build

# Production Stage
FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf -- *
COPY --from=build /bookcars/frontend/build .
COPY ./frontend/nginx.conf /etc/nginx/conf.d/default.conf

# Expose standard HTTP/HTTPS ports
EXPOSE 80
EXPOSE 443

CMD ["nginx", "-g", "daemon off;"]

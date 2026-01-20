# syntax=docker/dockerfile:1

FROM node:lts-alpine
WORKDIR /bookcars/backend

# Copy source
COPY ./backend ./ 
COPY ./packages /bookcars/packages

# Install dependencies
RUN npm install --force

# Use Dokploy-injected env vars at runtime, e.g., MONGO_URI, JWT_SECRET, ADMIN_EMAIL, etc.
# They are available automatically when you set them in the project settings.

# Start backend
CMD ["npm", "run", "start:setup"]

# Expose backend port
EXPOSE 4002

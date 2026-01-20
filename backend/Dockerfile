# syntax=docker/dockerfile:1

FROM node:lts-alpine AS production

# Build context = backend/
WORKDIR /bookcars/backend

# Copy everything from backend folder
COPY . .

# Install dependencies
RUN npm install --force

# Expose backend port
EXPOSE 4002

# Start BookCars backend
CMD ["npm", "run", "start:setup"]

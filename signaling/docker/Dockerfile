# docker/Dockerfile
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY ../package*.json ./

# Install dependencies
RUN npm install

# Copy the server.js file
COPY ../bin ./bin

# Expose the port the app runs on
EXPOSE 4444

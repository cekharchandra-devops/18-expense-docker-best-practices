* Mutli Stage Build

```
const express = require('express');
const app = express();
const port = 8080;

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(port, () => {
  console.log(`App running on http://localhost:${port}`);
});
```
```
{
  "name": "expense-backend",
  "version": "1.0.0",
  "description": "A simple Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```
Step 2: Create a Multi-Stage Dockerfile

```
# Stage 1: Build the Node.js application
FROM node:20 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the application source code
COPY package.json .
COPY index.js .

# Install dependencies
RUN npm install

# Stage 2: Create a minimal image to run the Node.js application
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the compiled binary from the builder stage
COPY --from=builder /app .

# Expose the application port
EXPOSE 8080

# Run the Node.js application
CMD ["npm", "start"]
```

Stage 1: Build the Node.js Application

FROM node:20 AS builder: Use the official Node.js image as the base image for the build stage.
WORKDIR /app: Set the working directory inside the container.
COPY package.json .: Copy the package.json file into the container.
COPY index.js .: Copy the index.js file into the container.
RUN npm install: Install the application dependencies.

Stage 2: Create a Minimal Image to Run the Application

FROM node:20-alpine: Use the official Node.js Alpine image as the base image for the final stage.
WORKDIR /app: Set the working directory inside the container.
COPY --from=builder /app .: Copy the application files from the builder stage.
EXPOSE 8080: Expose port 8080 for the application.
CMD ["npm", "start"]: Run the Node.js application.

Step 3: Build and Run the Docker Image
Build the Docker Image:
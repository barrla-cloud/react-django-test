# Use Node.js official image
FROM node:18-alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json /app/
RUN npm install

# Copy the entire project
COPY . /app/

# Build the React app
RUN npm run build

# Install the `serve` package to serve the build
RUN npm install -g serve

# Expose the port the app will run on
EXPOSE 5000

# Command to serve the built app
CMD ["serve", "-s", "build", "-l", "5000"]


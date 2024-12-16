# Step 1: Build the client (React + Vite app)
FROM node:20.18.1 as builder

# Set the working directory for the frontend build inside the container
WORKDIR /app/client

# Copy the package files for the frontend
COPY ./client/package.json ./client/package-lock.json ./

# Install frontend dependencies
RUN npm install

# Copy the rest of the client files
COPY ./client/ ./

# Build the frontend app (this will generate the dist folder)
RUN npm run build

# Step 2: Serve the built client with Nginx
FROM nginx:alpine

# Copy the built app (dist folder) from the builder stage to Nginx's default directory
COPY --from=builder /app/client/dist /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

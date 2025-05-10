

# Use a minimal Node.js image
FROM node:18-alpine

# Install http-server globally
RUN npm install -g http-server

# Set working directory
WORKDIR /app

# Copy HTML files to container
COPY . .

# Expose port for frontend
EXPOSE 8080

# Run the http-server
CMD ["http-server", "-p", "8080"]

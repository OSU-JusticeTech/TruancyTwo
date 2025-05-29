# Use a lightweight Node.js image
FROM docker.io/library/node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first (for better caching)
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --frozen-lockfile

# Copy the rest of the app files
COPY . .

# Build the React app
RUN npm run build

# Use Nginx to serve the built React app
FROM docker.io/library/nginx:alpine
COPY --from=0 /app/build /usr/share/nginx/html

COPY default.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

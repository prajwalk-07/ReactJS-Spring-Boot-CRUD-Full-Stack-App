# ---------- Stage 1: Build React ----------
FROM node:18-alpine AS builder
WORKDIR /app

# Copy and install dependencies
COPY package*.json ./
RUN npm install

# Copy project files and build production bundle
COPY . .
RUN npm run build

# ---------- Stage 2: Serve via Nginx ----------
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Remove default Nginx static files
RUN rm -rf ./*

# Copy build output from builder stage
COPY --from=builder /app/build .

# Expose the port Nginx serves
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

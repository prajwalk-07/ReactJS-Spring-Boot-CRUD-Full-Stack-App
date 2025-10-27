# ---------- Stage 1: Build React App ----------
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy project files and build production bundle
COPY . .

# ✅ Fix OpenSSL error for Node 17+
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# ---------- Stage 2: Serve via Nginx ----------
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/build .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# ---------- Stage 1: Build ----------
    FROM node:18-alpine AS builder

    WORKDIR /app
    
    # Copy only package files first (better caching)
    COPY package*.json ./
    
    RUN npm ci
    
    # Copy the rest of the source
    COPY . .
    
    # Build the frontend
    RUN npm run build
    
    # ---------- Stage 2: Runtime ----------
    FROM nginx:alpine
    
    # Remove default nginx static files
    RUN rm -rf /usr/share/nginx/html/*
    
    # Copy built assets from builder stage
    COPY --from=builder /app/dist /usr/share/nginx/html
    
    # Expose port 80
    EXPOSE 80
    
    # Start nginx
    CMD ["nginx", "-g", "daemon off;"]
    
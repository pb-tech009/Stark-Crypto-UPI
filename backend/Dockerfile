# ==========================================
# STAGE 1: Build & Dependencies Stage
# ==========================================
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install all dependencies
RUN npm install

# Copy all source files
COPY . .

# ==========================================
# STAGE 2: Final Production Stage (Lightweight)
# ==========================================
FROM node:18-alpine

WORKDIR /app

# Copy ONLY the node_modules and source code from the builder stage
# This keeps the image size very small
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app ./

# Set production environment
ENV PORT=5000
ENV NODE_ENV=production

# Expose backend port
EXPOSE 5000

# Use node direct instead of nodemon for production
CMD ["node", "index.js"]

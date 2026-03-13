# ==========================================
# STAGE 1: Build Stage
# ==========================================
# node:18-alpine image use kari che jethi image ni size nani rahe
FROM node:18-alpine AS build

# Docker container ni andar 'app' directory banavi
WORKDIR /app

# Pehla package files copy kari jethi 'npm install' cache thai shake
COPY package*.json ./

# Badhi libraries install kari
RUN npm install --legacy-peer-deps

# Akho code copy karyo
COPY . .

# Vite build command chalaviyo (Jene lidhe 'dist' folder banshe)
RUN npx vite build

# ==========================================
# STAGE 2: Production Stage
# ==========================================
# Nginx image no use karyo server banavva mate
FROM nginx:stable-alpine

# Build stage mathi 'dist' folder copy kari Nginx na path ma muki didhu
COPY --from=build /app/dist /usr/share/nginx/html

# Custom nginx configuration copy kari SPA routing mate
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Port 80 expose karyo
EXPOSE 80

# Nginx ne foreground ma chalu karyu
CMD ["nginx", "-g", "daemon off;"]


# Using node:alpine as base image
FROM node:20-alpine AS build

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy source code and build the project
COPY . .
RUN npm run build

# STAGE 2: Production
# Using nginx:alpine for a tiny final image (~20MB)
FROM nginx:alpine AS prod

# Copy custom nginx configuration if needed
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy the static build files from the previous stage
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Expose port 80 for the Nginx service
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]



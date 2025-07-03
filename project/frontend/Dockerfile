# Stage 1: Build the React app
FROM node:22.16.0-bullseye-slim AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install
RUN npm install @fortawesome/fontawesome-free

COPY . .

RUN npm run build

# Stage 2: Serve app with Nginx
FROM nginx:alpine

# Copy the build output from previous stage to Nginx html folder
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]


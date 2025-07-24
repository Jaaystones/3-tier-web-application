# Web-Tier Dockerfile using NGINX
# Step 1: Build the React app
FROM node:14-alpine AS  build

WORKDIR /web-tier
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2: Serve the app with NGINX
FROM nginx:alpine

COPY --from=build /web-tier/build /usr/share/nginx/html

# Copy custom NGINX configuration
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

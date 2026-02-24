# === Stage 1: Build the Angular application ===
FROM node:18 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install -g @angular/cli
RUN npm install
COPY . .
RUN ng build --configuration production

# === Stage 2: Serve the application with NGINX ===
FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
# Copy the built application files from the 'build' stage to the NGINX web server directory
COPY --from=build /app/dist/angular-15-crud/* /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

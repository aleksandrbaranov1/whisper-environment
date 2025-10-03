# Этап сборки фронта
FROM node:20-bullseye-slim as build

WORKDIR /app

COPY whisper-frontend2/package*.json ./
RUN npm install --legacy-peer-deps --quiet

COPY whisper-frontend2 .
RUN npm run build

# Этап nginx
FROM nginx:stable-alpine

COPY NGINX/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

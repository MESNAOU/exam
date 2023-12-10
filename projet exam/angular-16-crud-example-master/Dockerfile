# syntax=docker/dockerfile:1

FROM node:20.9.0-alpine3.18 as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build --prod

FROM nginx:alpine
ENV NODE_ENV production
# Ajout de configurations spécifiques pour les sondes
COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/angular-16-crud /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

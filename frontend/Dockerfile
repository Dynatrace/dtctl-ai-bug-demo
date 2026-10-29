FROM node:24-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
# nginx:alpine can lag Alpine security fixes; ensure brotli-libs >= 1.2.1 (CVE-2026-111497)
RUN apk upgrade --no-cache brotli-libs
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80

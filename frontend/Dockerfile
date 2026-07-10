# Сборка React-приложения
FROM node:18-alpine as build

WORKDIR /app

# Копируем package.json и устанавливаем зависимости
COPY package*.json ./
RUN npm install

# Копируем исходники и собираем приложение
COPY . .
RUN npm run build

# Раздача статики через Nginx
FROM nginx:1.22.1-alpine

# Копируем собранное приложение в Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Копируем конфиг Nginx (если есть)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

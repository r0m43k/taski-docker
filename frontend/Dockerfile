# Этап сборки фронтенда
FROM node:18-alpine AS build

WORKDIR /app

# Копируем package.json и lock-файл
COPY package*.json ./

# Устанавливаем зависимости
RUN npm ci

# Копируем остальной код
COPY . .

# Собираем production-сборку
RUN npm run build

# Этап рантайма — отдаём статику через nginx
FROM nginx:alpine

# Копируем собранный фронт в nginx
COPY --from=build /app/build /usr/share/nginx/html

# По умолчанию nginx слушает 80 порт
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

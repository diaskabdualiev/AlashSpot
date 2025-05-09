FROM node:20-alpine as builder

WORKDIR /app

# Установка pnpm
RUN npm install -g pnpm

# Копирование файлов зависимостей
COPY package.json pnpm-lock.yaml ./

# Установка зависимостей
RUN pnpm install --frozen-lockfile

# Копирование исходного кода
COPY . .

# Сборка приложения
RUN pnpm build

# Финальный образ
FROM node:20-alpine

WORKDIR /app

# Установка простого HTTP-сервера
RUN npm install -g serve

# Копирование собранного приложения
COPY --from=builder /app/build ./build

# Открытие порта
EXPOSE 3000

# Запуск приложения
CMD ["serve", "-s", "build", "-l", "3000"] 
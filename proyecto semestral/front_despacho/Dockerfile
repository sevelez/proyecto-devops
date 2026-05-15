# Etapa 1: Construcción
FROM node:20-alpine AS build
WORKDIR /app

# Instalar dependencias
COPY package*.json ./
RUN npm install

# Copiar código y construir
COPY . .
RUN npm run build

# Etapa 2: Servidor de producción con Nginx
FROM nginx:stable-alpine

# Copiar los archivos estáticos de Vite al directorio de Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponer el puerto 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

#test de cambio
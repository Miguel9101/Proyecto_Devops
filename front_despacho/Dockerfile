# ETAPA 1: Construcción (Build)
FROM node:18-alpine AS build
WORKDIR /app
# Copiamos los archivos de dependencias
COPY package*.json ./
# Instalamos las dependencias
RUN npm install
# Copiamos todo el código fuente
COPY . .
# Vite construye la carpeta /dist optimizada
RUN npm run build

# ETAPA 2: Producción (Servidor Nginx)
FROM nginx:alpine
# Copiamos lo que Vite construyó en la etapa anterior a Nginx
COPY --from=build /app/dist /usr/share/nginx/html
# Configuramos permisos para cumplir con el mínimo privilegio (no usar root)
RUN chown -R nginx:nginx /usr/share/nginx/html
USER nginx
# Exponemos el puerto 80
EXPOSE 80
# Encendemos Nginx
CMD ["nginx", "-g", "daemon off;"]
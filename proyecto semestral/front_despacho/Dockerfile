# ETAPA 1 -> BUILD
FROM node:20-alpine AS build
WORKDIR /app
# Copiar package files
COPY package*.json ./
# Instalar dependencias
RUN npm install
# Copiar código fuente
COPY . .
# Generar build producción
RUN npm run build
# =========================
# ETAPA 2 -> PRODUCCIÓN
# =========================
FROM nginxinc/nginx-unprivileged:stable-alpine

# Copiar build generado
COPY --from=build /app/dist /usr/share/nginx/html
# Puerto nginx
EXPOSE 8080
# Iniciar nginx
CMD ["nginx", "-g", "daemon off;"]
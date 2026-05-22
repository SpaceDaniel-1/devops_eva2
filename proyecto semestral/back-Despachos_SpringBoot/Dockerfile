# ETAPA 1 -> BUILD
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app
# Copiar pom primero para aprovechar cache
COPY Springboot-API-REST-DESPACHO/pom.xml .
# Descargar dependencias
RUN mvn dependency:go-offline -B
# Copiar código fuente
COPY Springboot-API-REST-DESPACHO/src ./src
# Compilar aplicación
RUN mvn clean package -DskipTests
# =========================
# ETAPA 2 -> PRODUCCIÓN
# =========================
FROM eclipse-temurin:17-jre-alpine
# Crear usuario no root
RUN addgroup -S spring && adduser -S spring -G spring
WORKDIR /app
# Copiar jar compilado
COPY --from=build /app/target/*.jar app.jar
# Cambiar permisos
RUN chown -R spring:spring /app
# Usuario no root
USER spring:spring
# Puerto backend
EXPOSE 8081
# Ejecutar aplicación
ENTRYPOINT ["java","-jar","app.jar"]
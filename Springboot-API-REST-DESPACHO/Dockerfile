# ETAPA 1: Construcción (Build con Maven)
FROM maven:3.9.4-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# ETAPA 2: Producción (Ejecución con JRE ligero)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Creamos un usuario sin privilegios por seguridad (no root)
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
# Copiamos el .jar
COPY --from=build /app/target/*.jar app.jar
# Exponemos el puerto de Despachos (8081)
EXPOSE 8081
# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
# ETAPA 1: Construcción (Build con Maven)
FROM maven:3.9.4-eclipse-temurin-17 AS build
WORKDIR /app
# Copiamos el pom.xml y descargamos las dependencias
COPY pom.xml .
# Copiamos el código fuente
COPY src ./src
# Compilamos el proyecto saltando las pruebas para que sea más rápido
RUN mvn clean package -DskipTests

# ETAPA 2: Producción (Ejecución con JRE ligero)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Creamos un usuario sin privilegios por seguridad (no root)
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
# Copiamos el archivo .jar generado en la etapa 1
COPY --from=build /app/target/*.jar app.jar
# Exponemos el puerto de Ventas
EXPOSE 8080
# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
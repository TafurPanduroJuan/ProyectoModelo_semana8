# ── Etapa 1: Build ──────────────────────────────────────────────
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copia el código fuente y compila
COPY src ./src
RUN mvn clean package -DskipTests -B

# ── Etapa 2: Runtime ─────────────────────────────────────────────
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copia solo el JAR generado
COPY --from=build /app/target/ProyectoModelo-0.0.1-SNAPSHOT.jar app.jar

# Render asigna el puerto vía variable de entorno $PORT
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
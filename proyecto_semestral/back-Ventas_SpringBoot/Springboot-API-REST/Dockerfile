# Etapa 1: Compilación
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

# Copiar el pom y descargar dependencias (para aprovechar el cache de Docker)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiar el código fuente y compilar el .jar
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Copiar solo el jar generado desde la etapa de build
COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto (el puerto 3001 corresponde a la api de ventas)
EXPOSE 3001

ENTRYPOINT ["java", "-jar", "app.jar"]
#test de cambios
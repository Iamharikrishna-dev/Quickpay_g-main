# Build stage
FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /workspace

COPY . .

ARG SERVICE_MODULE

RUN mvn clean package -DskipTests -pl ${SERVICE_MODULE} -am

# Runtime stage
FROM eclipse-temurin:21-jre

WORKDIR /app

# Important: Declare ARG again in runtime stage
ARG SERVICE_MODULE

COPY --from=build /workspace/${SERVICE_MODULE}/target/${SERVICE_MODULE}-1.0.0.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
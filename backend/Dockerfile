FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /workspace

COPY . .

ARG SERVICE_MODULE

RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

ARG SERVICE_MODULE

COPY --from=build /workspace/${SERVICE_MODULE}/target/${SERVICE_MODULE}-1.0.0.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
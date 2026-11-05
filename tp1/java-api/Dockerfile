# on compile tout d'abord

FROM maven:3.10.0-amazoncorretto-21-al2023 AS build
WORKDIR /app

COPY pom.xml .
COPY src/ ./src/

RUN mvn clean package -DskipTests

# on exécute ensuite

FROM amazoncorretto:21-alpine

WORKDIR /app

COPY --from=build /app/target/java-api-1.0.0.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
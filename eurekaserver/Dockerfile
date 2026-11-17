FROM maven:3.9-eclipse-temurin-24 AS build

WORKDIR /app

COPY .mvn/ .mvn/
COPY mvnw mvnw.cmd pom.xml ./

RUN ./mvnw dependency:go-offline -B --no-transfer-progress

COPY src/ src/
RUN ./mvnw clean package -DskipTests -B --no-transfer-progress

FROM eclipse-temurin:24-jre

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 9000

ENTRYPOINT ["java", "-jar", "app.jar"]


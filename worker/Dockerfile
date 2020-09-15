FROM maven:3.5-jdk-8-alpine as builder

WORKDIR /app
COPY pom.xml /app
RUN mvn dependency:resolve
COPY src /app/src
RUN mvn package

FROM openjdk:8-jre-alpine

WORKDIR /app
COPY --from=builder /app/target /app/target
CMD ["java", "-jar", "/app/target/worker-jar-with-dependencies.jar"]
FROM maven:3.5-jdk-8-alpine as builder

# Refactor this by using WORKDIR
RUN mkdir /app
COPY pom.xml /app
WORKDIR /app
RUN mvn dependency:resolve
COPY src /app/src
RUN mvn package

FROM openjdk:8-jre-alpine

RUN mkdir /app
#COPY test-data/node1/.actorchoreography /root/.actorchoreography
COPY --from=builder /app/target /app/target

CMD ["java", "-jar", "/app/target/worker-jar-with-dependencies.jar"]
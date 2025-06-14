#step-1 build
FROM ubuntu:20.04 AS builder

WORKDIR /app

COPY . .

RUN apt update && apt install -y maven openjdk-11-jdk && mvn clean package


#step-2 
FROM adoptopenjdk/openjdk11:alpine-jre

WORKDIR /app

COPY --from=builder /app/target/spring-boot-web.jar app.jar

ENTRYPOINT ["java","-jar","app.jar"]


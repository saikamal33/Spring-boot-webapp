FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive


WORKDIR /app


RUN apt-get update && apt-get install -y openjdk-17-jdk maven docker.io && rm -rf /var/lib/apt/lists/*


COPY pom.xml .


CMD ["mvn", "dependency:go-offline"]

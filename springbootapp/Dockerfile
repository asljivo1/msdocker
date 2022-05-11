# Build stage
FROM ubuntu:18.04 as build 

RUN apt-get -y update && \
    apt-get -y install git maven && \
    git clone https://github.com/kkenan/basic-microservices.git

ENV APPDIR /basic-microservices/spring-boot-app
WORKDIR ${APPDIR}

RUN mvn clean package

# Package stage
FROM openjdk:8-jdk-alpine as package

ENV APPDIR /basic-microservices/spring-boot-app

ARG JAR_FILE=target/*.jar
COPY --from=build ${APPDIR}/target/*.jar app.jar

ENV PORT 8080
EXPOSE ${PORT}

ENTRYPOINT ["java","-jar","/app.jar"]



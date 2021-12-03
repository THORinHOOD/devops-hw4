FROM maven:3.6.0-jdk-8-slim AS build-web-app
COPY src /home/web-app/src
COPY pom.xml /home/web-app
RUN mvn -f /home/web-app/pom.xml clean package -Pweb-app

FROM maven:3.6.0-jdk-8-slim AS build-init-base
COPY src /home/web-app/src
COPY pom.xml /home/web-app
RUN mvn -f /home/web-app/pom.xml clean package -Pinit-base

FROM openjdk:8-jre-slim as web-app
COPY --from=build-web-app /home/web-app/target/dostavimvse-0.0.1-SNAPSHOT.jar /usr/local/lib/web-app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/local/lib/web-app.jar"]

FROM openjdk:8-jre-slim as init-base
COPY --from=build-init-base /home/web-app/target/dostavimvse-0.0.1-SNAPSHOT.jar /usr/local/lib/web-app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/local/lib/web-app.jar"]

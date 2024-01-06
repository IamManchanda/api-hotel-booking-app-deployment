# Stage 1: Build the application
FROM maven:3.8.1-jdk-11 AS build
WORKDIR /usr/src/app
COPY src ./src
COPY pom.xml .
RUN mvn clean install -DskipTests

# Stage 2: Create the lightweight image
FROM gcr.io/distroless/java
COPY --from=build /usr/src/app/target/notificationService-jar-with-dependencies.jar /usr/src/app/notificationService-jar-with-dependencies.jar
WORKDIR /usr/src/app
ENV PATH="${PATH}:${JAVA_HOME}/bin"
ENTRYPOINT [ "java", "-jar", "/usr/src/app/notificationService-jar-with-dependencies.jar"]
# Use an official Gradle image to build the application
FROM gradle:7.3.3-jdk17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy Gradle project files
COPY build.gradle settings.gradle ./
COPY src ./src

# Build the application (create the JAR file)
RUN gradle build -x test

# Use an official OpenJDK runtime as a parent image
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file from the previous stage
COPY --from=build /app/build/libs/*.jar app.jar

# Expose the port the application runs on
EXPOSE 8080

# Run the JAR file
ENTRYPOINT ["java", "-jar", "app.jar"]

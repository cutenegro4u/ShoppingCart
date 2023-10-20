# Use a base Java image with Maven for building
FROM maven:3.6-jdk-11 AS builder

# Set the working directory
WORKDIR /app

# Copy the POM file and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Build the application
RUN mvn package

# Create a lightweight runtime image
FROM openjdk:11-jre-slim

# Set the working directory
WORKDIR /app

# Copy the JAR/WAR file from the builder stage to the runtime image
COPY --from=builder /app/target/shopieasy.war .

# Expose the port your application will run on
EXPOSE 8080

# Define the command to run your application
CMD ["java", "-jar", "shopieasy.war"]

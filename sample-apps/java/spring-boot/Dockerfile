# Stage 1: Build the application
FROM openjdk:11.0-jdk AS build

# Set the working directory
WORKDIR /app

# Copy Maven Wrapper scripts and pom.xml first to leverage Docker cache
COPY mvnw pom.xml ./
COPY .mvn .mvn

# Make the Maven Wrapper executable
RUN chmod +x mvnw

# Copy the source code
COPY src ./src

# Build the application using Spring Boot Maven plugin
RUN ./mvnw clean package -DskipTests

# Stage 2: Run the application
FROM openjdk:11.0-jre-slim

# Set the working directory
WORKDIR /app

# Copy the executable JAR from the build stage
COPY --from=build /app/target/demo-app-0.0.1-SNAPSHOT.jar ./demo-app.jar

# Expose port 8080
EXPOSE 8080

# Define the default command to run the application
CMD ["java", "-jar", "demo-app.jar"]

# Stage 1: Build Stage
FROM maven:3.9.4-eclipse-temurin-21 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy the Maven configuration files
COPY pom.xml .

# Download dependencies (caching layer)
RUN mvn dependency:go-offline -B

# Copy the application source code
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Stage 2: Runtime Stage
FROM eclipse-temurin:21-jdk-jammy AS runtime

# Set the working directory in the container
WORKDIR /app

# Copy only the packaged jar from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose the application port (adjust if necessary)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]



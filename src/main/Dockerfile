# Use a base image with Maven to build the application
FROM maven:3.5.4-jdk-8-alpine AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the all files to the container
ADD . /app

# Download the project dependencies
RUN mvn clean install

# Use a base image with Java and Tomcat pre-installed
FROM tomcat:9.0.76-jdk21-openjdk

# Set the working directory inside the container
WORKDIR /usr/local/tomcat/webapps

# Copy the generated WAR file to the container
COPY --from=builder /app/target/demo-1.0-SNAPSHOT.war ./ROOT.war

# Set a+rwx permissions to the new webapps directory
RUN chmod -R 777 /usr/local/tomcat/webapps

# Set a non-root user
USER 10014

# Start Tomcat when the container launches
CMD ["catalina.sh", "run"]

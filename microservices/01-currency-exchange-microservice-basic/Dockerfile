# Maven and JDK 8 - necessary for compiling and packaging a Java application 
FROM maven:3.8.2-jdk-8-slim AS build 
WORKDIR /home/app
COPY . /home/app
RUN mvn -f /home/app/pom.xml clean package

# A lightweight image containing JDK 8 runtime, suitable for running Java apps. 
FROM openjdk:8-jdk-alpine
#volume created inside container to store temp files 
VOLUME /tmp 
EXPOSE 8000
COPY --from=build /home/app/target/*.jar app.jar
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]
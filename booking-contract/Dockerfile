FROM eclipse-temurin:17-jdk-jammy
VOLUME /tmp
EXPOSE 8080
ARG JAR_FILE=target/booking-contract-1.0-SNAPSHOT.jar
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
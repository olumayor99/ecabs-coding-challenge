FROM eclipse-temurin:17-jdk-jammy as build
WORKDIR /opt/app
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:go-offline
COPY ./src ./src
RUN ./mvnw clean install

FROM eclipse-temurin:17-jre-jammy
RUN addgroup producer; adduser  --ingroup producer --disabled-password producer
USER producer
WORKDIR /opt/app
ENV SPRING_RABBITMQ_HOST=$SPRING_RABBITMQ_HOST\
    SPRING_RABBITMQ_PORT=$SPRING_RABBITMQ_PORT\
    SPRING_RABBITMQ_USER=$SPRING_RABBITMQ_USER\
    SPRING_RABBITMQ_PASS=$SPRING_RABBITMQ_PASS\
    SPRING_MAIN_ABDO=$SPRING_MAIN_ABDO 

EXPOSE 8080
COPY --from=build /opt/app/target/*.jar /opt/app/*.jar
ENTRYPOINT ["java", "-jar", "/opt/app/*.jar" ]
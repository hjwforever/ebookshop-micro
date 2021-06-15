FROM openjdk:8-jdk-alpine as mvn-build
WORKDIR /app/build
COPY ./src ./src
COPY pom.xml .
COPY .mvn .mvn
COPY mvnw .
#COPY . .
#RUN ./mvn -N io.takari:maven:wrapper -Dmaven=3.6.3
#RUN apt-get update && apt-get install dos2unix
#RUN chmod +x mvnw
RUN sed -i 's/\r$//' mvnw
RUN ./mvnw clean install -Dmaven.test.skip=true

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=mvn-build /app/build/target/*.jar ./spring-app.jar
CMD ["java", "-jar", "/app/spring-app.jar"]

#FROM openjdk:8-jdk-alpine
#VOLUME /tmp
#ADD target/*.jar server.jar
#ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/server.jar"]
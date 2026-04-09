FROM eclipse-temurin:17-jdk
WORKDIR /app
ADD ./target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]

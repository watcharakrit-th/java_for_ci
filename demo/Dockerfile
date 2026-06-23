FROM eclipse-temurin:21-jre

WORKDIR /app
COPY target/*.jar app.jar

RUN useradd -r -u 1000 appuser
USER appuser

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

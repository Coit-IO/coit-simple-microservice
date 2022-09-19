FROM openjdk:8-jdk-alpine
# Environment Variable that defines the endpoint of sentiment-analysis python api.
ENV SA_LOGIC_API_URL http://localhost:5000
EXPOSE 8080
WORKDIR /usr/app
CMD ["java", "-jar", "/usr/app/sentiment-analysis-web-0.0.2-SNAPSHOT.jar", "--sa.logic.api.url=${SA_LOGIC_API_URL}"]
COPY target/sentiment-analysis-web-0.0.2-SNAPSHOT.jar /usr/app
# RUN adduser -D basil && chmod 755 /usr/app/sentiment-analysis-web-0.0.2-SNAPSHOT.jar && mkdir /usr/app/uploads && chown -R basil /usr/app/uploads
# USER basil

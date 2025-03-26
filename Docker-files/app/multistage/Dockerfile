# Use lowercase stage name (Docker best practice)
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build-stage

# Clone and build
RUN git clone https://github.com/Kalai25-tech/dev.git /app && \
    cd /app && \
    git checkout dev && \
    mvn clean install

FROM tomcat:10-jdk21
RUN rm -rf /usr/local/tomcat/webapps/*

# Fix: Copy from correct path (/app/target/... instead of vprofile-project/target/...)
COPY --from=build-stage /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]

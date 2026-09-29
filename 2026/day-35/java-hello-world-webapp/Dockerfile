FROM maven:3.9.12-eclipse-temurin-17 AS build

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests #creates the war file 

RUN ls -a

FROM tomcat:10.1-jre17-temurin-jammy

COPY --from=build /app/target/java-hello-world.war /usr/local/tomcat/webapps/

RUN groupadd appgroup && useradd -g appgroup appuser

RUN chown -R appuser:appgroup /usr/local/tomcat
# switch to /appuser and take ownership and run file inside /usr/local/tomcat
USER appuser 

EXPOSE 8080
# catalina.sh starts the tomcat server and tomcat finds and deploys your .war application.
CMD ["catalina.sh","run"] 

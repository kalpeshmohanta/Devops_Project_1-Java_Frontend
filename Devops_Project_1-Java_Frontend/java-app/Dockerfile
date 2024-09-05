FROM maven:3.6.1-jdk-11-slim AS build

COPY src /home/app/src

COPY pom.xml /home/app

RUN mvn -f /home/app/pom.xml clean package



FROM openjdk:20-slim-buster

RUN mkdir /opt/tomcat

WORKDIR /opt/tomcat

ADD https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.5/bin/apache-tomcat-10.1.5.tar.gz .

RUN tar -xvzf apache-tomcat-10.1.5.tar.gz

RUN mv apache-tomcat-10.1.5/* /opt/tomcat

EXPOSE 8080

COPY --from=build /home/app/target/maven.war /opt/tomcat/webapps/

CMD ["/opt/tomcat/bin/catalina.sh", "run"]


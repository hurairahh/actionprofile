#FROM maven:3.9.9-eclipse-temurin-21-jammy AS BUILD_IMAGE
#COPY . /app
#WORKDIR /APP
#RUN mvn install


#FROM tomcat:10-jdk21

#RUN rm -rf /usr/local/tomcat/webapps/*

#COPY --from=BUILD_IMAGE vprofile-project/app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

#EXPOSE 8080
#CMD ["catalina.sh", "run"]



FROM maven:3.9.9-eclipse-temurin-21-jammy AS build_image

WORKDIR /app
COPY . .
RUN mvn clean install -DskipTests


FROM tomcat:10-jdk21

# Remove default WARs
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy generated WAR from build stage
COPY --from=build_image /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
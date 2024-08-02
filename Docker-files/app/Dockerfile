FROM openjdk:11 AS build_image

RUN apt update && apt install maven -y
RUN git clone https://github.com/parimal5/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install


FROM tomcat:9-jre11
LABEL "project"="VProfile"
LABEL "Author"="Parimal"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build_image vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war


# default no need to mentioned explictely
EXPOSE 8080
CMD [ "catalina.sh" , "run" ]
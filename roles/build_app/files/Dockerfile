# Building a java-war application
FROM maven:3.8.1-jdk-11 AS builder
WORKDIR /tmp
RUN git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git
WORKDIR /tmp/boxfuse-sample-java-war-hello
RUN mvn package


FROM alpine:3.13
# Install Tomcat 9
RUN apk add openjdk8-jre \
    && wget http://apache.rediris.es/tomcat/tomcat-9/v9.0.46/bin/apache-tomcat-9.0.46.tar.gz -O /tmp/tomcat9.tar.gz \
    && mkdir /opt/tomcat \
    && tar xvzf /tmp/tomcat9.tar.gz  --strip-components 1 --directory /opt/tomcat \
    && rm /tmp/tomcat9.tar.gz

# Copy artifacts
WORKDIR /opt/tomcat/webapps
COPY --from=builder /tmp/boxfuse-sample-java-war-hello/target/hello-1.0.war .

# Container launch conditions
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]

# Use an official java image with OpenJDK 6
FROM java:6

MAINTAINER lzilber

ENV MAVEN_HOME /opt/apache-maven-2.2.1
ENV SONAR_HOME /opt/sonar-2.0.1

# Install sonar and maven in /opt
WORKDIR /opt
RUN set -x \
	&& wget http://downloads.sonarsource.com/sonarqube/sonar-2.0.1.zip \
	&& unzip ./sonar-2.0.1.zip \
	&& rm ./sonar-2.0.1.zip \
	&& wget http://archive.apache.org/dist/maven/binaries/apache-maven-2.2.1-bin.zip \
	&& unzip ./apache-maven-2.2.1-bin.zip \
	&& rm ./apache-maven-2.2.1-bin.zip

# Update maven settings with the sonar profile
COPY maven-settings.xml /opt/apache-maven-2.2.1/conf/settings.xml

# sonar.sh uses the 'ps' command
RUN apt-get update && apt-get install -y \
    procps

# Fetch a maven 2 project in /tmp
WORKDIR /tmp
RUN set -x \
        && wget http://archive.apache.org/dist/commons/logging/source/commons-logging-1.1.1-src.zip \
        && unzip ./commons-logging-1.1.1-src.zip \
        && rm ./commons-logging-1.1.1-src.zip 

# Http port
EXPOSE 9000

# Derby Database port
EXPOSE 1527

# Start sonar 
WORKDIR ${SONAR_HOME}
CMD ["./bin/linux-x86-64/sonar.sh","start"]

# Next we should run the maven analysis
# cd /tmp
# cd commons-logging-1.1.1-src
# $MAVEN_HOME/bin/mvn clean install 
# $MAVEN_HOME/bin/mvn sonar:sonar
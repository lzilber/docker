# Use a Debian (Ubuntu 14.04) distribution with jdk 1.5
FROM lwis/java5

MAINTAINER lzilber

ENV MAVEN_HOME /opt/apache-maven-2.2.1
ENV SONAR_HOME /opt/sonar-1.5.1

# Required packages : unzip
RUN apt-get install unzip

# Install sonar and maven in /opt
WORKDIR /opt
RUN set -x \
	&& wget http://downloads.sonarsource.com/sonarqube/sonar-1.5.1.zip \
	&& unzip ./sonar-1.5.1.zip \
	&& rm ./sonar-1.5.1.zip \
	&& wget http://archive.apache.org/dist/maven/binaries/apache-maven-2.2.1-bin.zip \
	&& unzip ./apache-maven-2.2.1-bin.zip \
	&& rm ./apache-maven-2.2.1-bin.zip

# Update maven settings with the sonar profile
COPY maven-settings.xml /opt/apache-maven-2.2.1/conf/settings.xml

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

# Start sonar 1.5.1 
WORKDIR ${SONAR_HOME}
CMD ["./bin/linux-x86-64/sonar.sh","start"]

# Next we should setup the sonar database and run the maven analysis with the sonar 1.5.1 plugin
# cd /tmp
# wget http://localhost:9000/setup/setup_database
# cd commons-logging-1.1.1-src
# $MAVEN_HOME/bin/mvn clean install org.codehaus.sonar:sonar-maven-plugin:1.5.1:sonar

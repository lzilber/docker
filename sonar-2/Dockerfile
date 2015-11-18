# Use an official java image with OpenJDK 6
FROM java:6

MAINTAINER lzilber

# sonar.sh uses the 'ps' command
RUN apt-get update && apt-get install -y \
    procps

# Fetch a maven project in /tmp
WORKDIR /tmp
RUN set -x \
	&& wget http://archive.apache.org/dist/commons/logging/source/commons-logging-1.1.1-src.zip \
        && unzip ./commons-logging-1.1.1-src.zip \
        && rm ./commons-logging-1.1.1-src.zip 

# Set the versions and paths
ENV MAVEN_VERSION=2.2.1 
ENV MAVEN_HOME=/opt/apache-maven-${MAVEN_VERSION}
ENV JAVA_HOME=/usr/lib/jvm/java-6-openjdk-amd64/

# Install sonar and maven in /opt
WORKDIR /opt
RUN set -x \
    && wget http://archive.apache.org/dist/maven/binaries/apache-maven-${MAVEN_VERSION}-bin.zip \
	&& unzip ./apache-maven-${MAVEN_VERSION}-bin.zip \
	&& rm ./apache-maven-${MAVEN_VERSION}-bin.zip

ENV SONAR_VERSION=2.9 
ENV SONAR_HOME=/opt/sonar-${SONAR_VERSION}
RUN set -x \
	&& wget http://downloads.sonarsource.com/sonarqube/sonar-${SONAR_VERSION}.zip \
	&& unzip ./sonar-${SONAR_VERSION}.zip \
	&& rm ./sonar-${SONAR_VERSION}.zip

# Update maven settings with the sonar profile
COPY maven-settings.xml /opt/apache-maven-${MAVEN_VERSION}/conf/settings.xml

# Http port
EXPOSE 9000

# Derby Database port
EXPOSE 1527

# Prepare the maven analysis
# NOTE : still using maven 2
WORKDIR /tmp/commons-logging-1.1.1-src
RUN $MAVEN_HOME/bin/mvn clean install

# Start sonar 
WORKDIR ${SONAR_HOME}
CMD ["./bin/linux-x86-64/sonar.sh","start"]

# Next we should run the maven analysis
# cd /tmp
# cd commons-logging-1.1.1-src
# $MAVEN_HOME/bin/mvn sonar:sonar
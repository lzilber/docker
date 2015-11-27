# Use a Debian (Ubuntu 14.04) distribution with jdk 1.5
FROM lwis/java5

MAINTAINER lzilber

# Required packages : unzip
RUN apt-get install unzip

# Fetch a maven project in /tmp
WORKDIR /tmp
RUN set -x \
	&& wget http://archive.apache.org/dist/commons/logging/source/commons-logging-1.1.1-src.zip \
        && unzip ./commons-logging-1.1.1-src.zip \
        && rm ./commons-logging-1.1.1-src.zip 

# Set the versions and paths
ENV MAVEN_VERSION=2.2.1 
ENV MAVEN_HOME=/opt/apache-maven-${MAVEN_VERSION}
#ENV JAVA_HOME=/jdk1.5.0_22

# Install sonar and maven in /opt
WORKDIR /opt
RUN set -x \
    && wget http://archive.apache.org/dist/maven/binaries/apache-maven-${MAVEN_VERSION}-bin.zip \
	&& unzip ./apache-maven-${MAVEN_VERSION}-bin.zip \
	&& rm ./apache-maven-${MAVEN_VERSION}-bin.zip

ENV SONAR_VERSION=1.5.1
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
# $MAVEN_HOME/bin/mvn org.codehaus.sonar:sonar-maven-plugin:1.5.1:sonar
# Use an official java image with OpenJDK 7
FROM java:7

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
ENV MAVEN_VERSION=3.3.3 
ENV MAVEN_HOME=/opt/apache-maven-${MAVEN_VERSION}
ENV JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/

# Install maven in /opt
WORKDIR /opt
RUN set -x \
    && wget http://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.zip \
	&& unzip ./apache-maven-${MAVEN_VERSION}-bin.zip \
	&& rm ./apache-maven-${MAVEN_VERSION}-bin.zip

# Update maven settings with the sonar profile
#COPY maven-settings.xml /opt/apache-maven-${MAVEN_VERSION}/conf/settings.xml

# Prepare the maven analysis
WORKDIR /tmp/commons-logging-1.1.1-src
RUN $MAVEN_HOME/bin/mvn clean install

# Install sonar in /opt
WORKDIR /opt
ENV SONAR_VERSION=5.2
ENV SONAR_HOME=/opt/sonarqube-${SONAR_VERSION}
RUN set -x \
	&& wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-${SONAR_VERSION}.zip \
	&& unzip ./sonarqube-${SONAR_VERSION}.zip \
	&& rm ./sonarqube-${SONAR_VERSION}.zip

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
# $MAVEN_HOME/bin/mvn sonar:sonar -Dsonar.scm.disabled=True
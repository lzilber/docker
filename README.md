# docker

## This is not the container you are looking for

All the containers have been created for a very specific purpose (screenshots). They embed a sample project to be analysed, which is probably something you do not need. The Official SonarQube docker is more likely the docker container you need.
![alt text](https://github.com/lzilber/docker/obiwan-hand.png "Obiwan's gesture")

## sonar-1.5

This image is intended for simple screenshots and testing of SonarQube legacy version 1.5.1 (released Jan. 9 2009).

Based on a Java 5 image (Ubuntu 14.04, see lwis/java5), this image provides :
 * sonar 1.5.1 with the default Derby database.
 * maven 2.2.1 (required to analyse a java project with org.codehaus.sonar:sonar-maven-plugin:1.5.1)
 * a sample "maven 2-compatible" project for analysis : commons-logging-1.1.1 

Usage notes:
 1. Setup the sonar database to complete the installation (Open a browser on your docker exposed IP and PORT and click the setup/setup_database link)
 2. Run the maven analysis with the sonar 1.5.1 plugin : mvn clean install org.codehaus.sonar:sonar-maven-plugin:1.5.1:sonar

## sonar-2.0

Image to test SonarQube legacy version 2.0.1 (released Mar. 10, 2010).

Based on a Java 6 image (OpenJDK 6), this image provides :
 * sonar 2.0.1 with the default Derby database.
 * maven 2.2.1 
 * a sample "maven 2-compatible" project for analysis : commons-logging-1.1.1 

Usage notes:
 * Run the maven analysis in the project root (/tmp/commons-logging-1.1.1-src) : 
   * $MAVEN_HOME/bin/mvn clean install
   * $MAVEN_HOME/bin/mvn sonar:sonar

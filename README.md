# docker (SonarQube docker images)

![alt text](https://raw.githubusercontent.com/lzilber/docker/master/obiwan-hand.png "Obiwan's gesture")

## This is not the container you are looking for

All the containers have been created for a very specific purpose (screenshots). They embed a sample project to be analysed, which is probably something you do not need. The [Official SonarQube docker](https://hub.docker.com/_/sonarqube/) is more likely the docker container you need.

## sonarqube-5

Used to build images of SonarQube version 5.x (starting at 5.0.1 released Feb. 24 2015).

Note: Analysis for 5.0 and 5.1 requires the option -Dsonar.scm.disabled=True

| Component | Version |
| --------- | ------- |
| Java  | 7  |
| Maven  | 3.3.3  |

## sonar-2

Used to build images of SonarQube legacy version 2.x to 4.x (including LTS 4.5.6).

Setup maven 2 and a "maven 2-compatible" project commons-logging-1.1.1.

| Component | Version |
| --------- | ------- |
| Java  | 6  |
| Maven  | 2.2.1  |

## sonar-1.x

Used to build images of SonarQube legacy version 1.5.1 (released Jan. 9 2009) to 1.14 .

| Component | Version |
| --------- | ------- |
| Java  | 6 (except for 1.5.1 see below)  |
| Maven  | 2.2.1  |

### version 1.5.1

Based on a Java 5 image (Ubuntu 14.04, see lwis/java5), this image provides :
 * sonar 1.5.1 with the default Derby database.
 * maven 2.2.1 (required to analyse a java project with org.codehaus.sonar:sonar-maven-plugin:1.5.1)
 * a sample "maven 2-compatible" project for analysis : commons-logging-1.1.1 

Usage notes:
 1. Setup the sonar database to complete the installation (Open a browser on your docker exposed IP and PORT and click the setup/setup_database link)
 2. Run the maven analysis with the sonar 1.5.1 plugin : mvn clean install org.codehaus.sonar:sonar-maven-plugin:1.5.1:sonar

## sonar-2.0

Used to build an image to test SonarQube legacy version 2.0.1 (released Mar. 10, 2010).

Based on a Java 6 image (OpenJDK 6), this image provides :
 * sonar 2.0.1 with the default Derby database.
 * maven 2.2.1 
 * a sample "maven 2-compatible" project for analysis : commons-logging-1.1.1 

Usage notes:
 * Run the maven analysis in the project root (/tmp/commons-logging-1.1.1-src) : 
   * $MAVEN_HOME/bin/mvn clean install
   * $MAVEN_HOME/bin/mvn sonar:sonar

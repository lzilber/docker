# docker

## sonar-1.5

This image is intended for simple screenshots and testing of SonarQube legacy version 1.5.1 (released Jan. 9 2009).

Based on a Java 5 image (Ubuntu 14.04), this image provides :
 * sonar 1.5.1 with the default Derby database.
 * maven 2.2.1 (required to analyse a java project with org.codehaus.sonar:sonar-maven-plugin:1.5.1)
 * a sample "maven 2-compatible" project for analysis : commons-logging-1.1.1 

Usage notes:
 1. Setup the sonar database to complete the installation (Open a browser on your docker exposed IP and PORT and click the setup/setup_database link)
 2. Run the maven analysis with the sonar 1.5.1 plugin : mvn clean install org.codehaus.sonar:sonar-maven-plugin:1.5.1:sonar

# Sonarqube
Sonarqube installation pre-requisites
A VM with minimum of 2 gb of RAM ( AWS t3.medium)
Docker and docker-compose installed and docker service running

Install Sonarqube using the docker-composefile
docker-compose up -d 

Once Sonarqube is up and running can be accessed using URL : http://<<IP address>>:9000
Default username and password : admin:admin

Create a Project in Sonarqube and note down the project key

In Jenkins install the sonarqube  scanner plugin 
1. From the Jenkins Dashboard, navigate to Manage Jenkins > Manage Plugins and install the SonarQube Scanner plugin.
2. Back at the Jenkins Dashboard, navigate to Credentials > System from the left navigation.
3. Click the Global credentials (unrestricted) link in the System table.
4. Click Add credentials in the left navigation and add the following information:
      Kind: Secret Text
      Scope: Global
      Secret: Generate a token at User > My Account > Security in SonarQube, and copy and paste it here.
    Click OK.
5. From the Jenkins Dashboard, navigate to Manage Jenkins > Configure System.
6. From the SonarQube Servers section, click Add SonarQube. Add the following information:
7. Name: Give a unique name to your SonarQube instance.
8. Server URL: Your SonarQube instance URL.
9. Credentials: Select the credentials created during step 4.
10. Click Save
  
In Jenkins install GitHub Branch Source plugin version 2.7.1 or later is required

1. From the Jenkins Dashboard, navigate to Manage Jenkins > Manage Plugins and install the GitHub Branch Source plugin.
2. From the Jenkins Dashboard, navigate to Manage Jenkins > Configure System.
3. From the GitHub or GitHub Enterprise Servers section, add your GitHub server.
4. Click Save.

In Jenkins global tool configuration. Add Sonar Scanner tool and allow it automatically install the binary

In the Maven based application build pom.xml add the following under build management -> plugins and push the changes to Github
          <plugin>
        <groupId>org.sonarsource.scanner.maven</groupId>
        <artifactId>sonar-maven-plugin</artifactId>
        <version>3.7.0.1746</version>
      </plugin>

  
add a build step Execute SonarQube  Scanner and add the below in additonal properties field
  sonar.host.url=URL
sonar.login=Personal Access token
sonar.projectKey=Project Key
sonar.java.binaries=PATH where Java compiled files are present
  

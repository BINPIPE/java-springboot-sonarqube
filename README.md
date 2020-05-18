# java-springboot-sonarqube
Sample Java Springboot Project to Demonstrate Declarative CI/CD Pipeline in Jenkins with SonarQube Quality Gates. 
++ Adding Slack Alerts to CI/CD declarative pipeline has also been included. Refer ++ below.


`Learning Resources for DevOps, SRE, Cloud & Engineering Management`

[![BINPIPE](https://img.shields.io/badge/BINPIPE-YouTube-red)](https://www.youtube.com/channel/UCPTgt4Wo0MAnuzNEEZlk90A)
[![Learn DevOps!](https://img.shields.io/badge/BINPIPE-Learn--DevOps-orange)](https://github.com/BINPIPE/resources/blob/master/devops-lesson-plans.md)
[![BINPIPE](https://img.shields.io/badge/Live--Classroom-blue)](https://forms.gle/tDJxDyj2nJyfsgsk7)
---

**Prerequisites**
```
-Install the below in Jenkins Server:
sudo apt install default-jdk
sudo apt install maven

-Run Sonarqube as Docker Container:
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

//Default credentials for SonarQube dashboard- admin/admin
```

**Configuring SonarQube Integration & Analysis to CI/CD Pipeline**

Follow the video for configuring the declarative pipeline with SonarQube Integration & Analysis.


Before running the Job ensure the following code snippets are added to the pom.xml file in order to Run Sonar Tests:

1. To be added inside <dependencies> block-

```
<!-- https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin -->
		<dependency>
			<groupId>org.sonarsource.scanner.maven</groupId>
			<artifactId>sonar-maven-plugin</artifactId>
			<version>3.2</version>
		</dependency>
		<!-- sonar block ends -->
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
                
  ```
  2. Profiles block to be added after </dependencies> block (replace the IP with the IP adress of your Sonar Server)-
  
  ```
  <!-- Profile added for Sonar -->
	<profiles>
<profile>
<id>sonar</id>
<activation>
<activeByDefault>true</activeByDefault>
</activation>
<properties>
<!-- Optional URL to server. Default value is http://localhost:9000 -->
<sonar.host.url>
http://192.168.0.155:9000
</sonar.host.url>
</properties>
</profile>
</profiles>
<!-- Profile ends for Sonar -->
  ```
  
  


The following code snippet is added to the Jenkins Pipeline script:


```
pipeline {
        agent any
        stages {

        stage("Source") {
          agent any
          steps {
              git branch: 'master', url: 'https://github.com/BINPIPE/java-springboot-sonarqube.git'
          }
        }

        
          stage("Build") {
            agent any
            steps {
                sh 'mvn clean package'
            }
          }

          stage("SonarQube Analysis") {
            agent any  
            steps {
              sh 'mvn sonar:sonar'
            }
          }

          stage('Approve Deployment') {
              agent any
              input{
                   message "Do you want to proceed for deployment?"
                      }
              steps {
                  //Add deploy steps & Alerts below
                  sh 'echo "Deploying into Server"' 

                }
          } 
          
        }
        
}


```





++ **Slack Alerts in CI/CD Pipeline**

The following snippet enables the slack-alerts stage in the CI/CD pipeline. 
Watch the video to see the configurations and the `Jenkins-Slack` Integration Process.

```
//Add this after the "stage" blocks end.

post {

    aborted {

      echo "Sending message to Slack"
      slackSend (color: "${env.SLACK_COLOR_WARNING}",
                 channel: "${params.SLACK_CHANNEL_2}",
                 message: "*ABORTED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
    } // aborted

    failure {

      echo "Sending message to Slack"
      slackSend (color: "${env.SLACK_COLOR_DANGER}",
                 channel: "${params.SLACK_CHANNEL_2}",
                 message: "*FAILED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
    } // failure

    success {
      echo "Sending message to Slack"
      slackSend (color: "${env.SLACK_COLOR_GOOD}",
                 channel: "${params.SLACK_CHANNEL_1}",
                 message: "*SUCCESS:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
    } // success

  } // post

```


<pre>
<a href="https://www.binpipe.org">BINPIPE</a> aims to simplify learning for those who are looking to make a foothold in the industry.
Write to me at <b>nixgurus@gmail.com</b> if you are looking for tailor-made training sessions.
For self-study resources look around in this repository, <a href="https://www.binpipe.org/">the Binpipe Blog</a> and <a href="https://www.youtube.com/channel/UCPTgt4Wo0MAnuzNEEZlk90A">Youtube Channel</a>.
</pre>

___
:ledger: Maintainer: **[Prasanjit Singh](https://www.linkedin.com/in/prasanjit-singh)** | **www.binpipe.org**
___

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)


pipeline {
        agent none
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

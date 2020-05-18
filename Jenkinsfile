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
          
        } // stage
        
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
        
        
        
        
      }

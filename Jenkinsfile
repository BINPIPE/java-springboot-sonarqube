def userInput = true
def didTimeout = false
node ('master'){ 
    stage('Checkout'){
        git branch: 'master', url: 'https://github.com/BINPIPE/java-springboot-sonarqube.git'
    }

    stage('Build'){
        //sh 'mvn clean package -Dmaven.test.skip=true -U'
        sh 'mvn clean install'
    }
    
    stage('Sonar Scan'){
        
        sh "mvn sonar:sonar -Dmaven.test.skip=true"
    }
    
        stage("Quality Gate"){
            
    timeout(time: 1, unit: 'MINUTES') { //---Just in case something goes wrong, pipeline will be killed after a timeout
    sleep 10 //---Allow time for Sonar Scan to be over in Server (To Do: Replace this with webhook!)
            def qg = waitForQualityGate() //--Reuse taskId previously collected by withSonarQubeEnv
                  if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
                  
    }
  }
}
    stage('Deploy'){
        sh 'echo Moving ahead with Deployment to Endpoints!'

    }
  }

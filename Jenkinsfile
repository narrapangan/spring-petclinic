pipeline {
  agent any
  stages {
    
    stage('Build') {
      steps {
        sh './mvnw package'
      }
    }
    
    stage('Test'){
        steps{
         sh 'mvn test'
        }
    }
    
     stage('Deploy') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    retry(5) {
                        sh 'mvn clean install'
                    }
                }
            }
        }
  }
  post{
    always{
   slackSend color: 'good', message: 'Message from Jenkins Pipeline'
    }
  }
}

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
         sh './mvn test'
        }
    }
    
     stage('Deploy') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    retry(5) {
                        sh './mvn deploy'
                    }
                }
            }
        }
  }
  post{
    always{
    slackSend "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
    }
  }
}

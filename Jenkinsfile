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
         sh 'echo "Fail!"; exit 1'
        }
    }
    
     stage('Deploy') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    retry(5) {
                        sh './flakey-deploy.sh'
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

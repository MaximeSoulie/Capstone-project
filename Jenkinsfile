pipeline {
  agent any
  stages {
    stage('switch to deploy folder') {
      steps {
        dir(path: 'Capstone-project/2-Build_and_Deploy/') {
          validateDeclarativePipeline 'Capstone-project/2-Build_and_Deploy/Jenkinsfile'
        }

      }
    }

  }
}
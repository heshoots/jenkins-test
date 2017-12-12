pipeline {
  agent none

  stages {
    stage('Test') {
      agent { dockerfile true }
      steps {
        sh """
          npm install
          npm run lint
        """
      }
    }
  }
}

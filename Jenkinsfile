pipeline {
  agent none

  stages {
    stage('Test') {
      agent {
        docker { dockerfile true }
      }
      steps {
        sh """
          npm install
          npm run lint
        """
      }
    }
  }
}

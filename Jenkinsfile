pipeline {
  agent none

  stages {
    stage('Test') {
      agent {
        docker { image 'node:9.21' }
      }
      steps {
        sh """
          npm install
          npm run lint
        """
      }
    }
    stage('build final image') {
      agent {
        docker { image 'docker:17.11.0-ce' }
      }
      steps {
        sh """
        docker build -f Dockerfile.prod -t quorauk/testapi:\$(cat version) .
        USER=\$(cat /docker/username.txt)
        PASS=\$(cat /docker/password.txt)
        echo "\$pass" | docker login --username \$USER --password \$PASS
        docker push quorauk/testapi:\$(cat version)
        """
      }
    }
  }
}

podTemplate(label: 'mypod', containers: [
  containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')
  ]) {
  node('mypod') {
    git 'https://github.com/heshoots/jenkins-test'
    stage('Build test image') {
      container('docker') {
        sh """
        ls
        docker build -f Dockerfile.test -t nodetest .
        """
      }
    }
    stage('run test image') {
      container('docker') {
        sh """
        docker run -it nodetest
        """
      }
    }
  }
}

podTemplate(label: 'mypod', containers: [
  containerTemplate(name: 'node', image: 'node:9.2.1', ttyEnabled: true, command: 'cat'),
  containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')
  ]) {
  node('mypod') {
    git 'https://github.com/heshoots/jenkins-test'
    stage('Test') {
      container('node') {
        sh """
        npm install
        npm run lint
        """
      }
    }
    stage('build final image') {
      app = docker.build("test")
    }
  }
}

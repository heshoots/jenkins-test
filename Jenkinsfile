podTemplate(label: 'mypod', containers: [
  containerTemplate(name: 'node', image: 'node:9.2', ttyEnabled: true, command: 'cat'),
  containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')
  ]) {
  node('mypod') {
    stage('lint') {
      git 'https://github.com/heshoots/jenkins-test'
      container('node') {
        sh """
        npm install --only-dev
        ./node_modules/.bin/eslint .
        """
      }
    }
    stage('Build image') {
      container('docker') {
        sh """
        ls
        docker build .
        """
      }
    }
  }
}

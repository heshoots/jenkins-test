podTemplate(label: 'mypod', containers: [
  containerTemplate(name: 'node', image: 'node:9.2', ttyEnabled: true, command: 'cat')
  ]) {
  node('mypod') {
    stage('Run shell') {
      git 'https://github.com/heshoots/jenkins-test'
      container('node') {
        sh """
        npm install --only-dev
        ./node_modules/.bin/eslint .
        """
      }
    }
  }
}

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
        node -p "require('./package.json').version" > version
        """
      }
    }
    stage('build final image') {
      container('docker') {
        sh """
        docker build -f Dockerfile.prod -t quorauk/testapi:\$(cat version) .
        USER=\$(cat /docker/username.txt)
        PASS=\$(cat /docker/password.txt)
        docker login --username \$USER --password \$PASS
        docker push quorauk/testapi:\$(cat version)
        """
      }
    }
  }
}

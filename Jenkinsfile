podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def imageName = "quorauk/testimage"
  node('docker') {
    git 'https://github.com/heshoots/jenkins-test'
    stage('Build test image') {
      container('docker') {
        sh """
        docker build -f Dockerfile.test -t ${imageName} .
        docker run --rm quorauk/testimage sh -c 'npm run lint'
        """
      }
    }
    stage('Upload image') {
      container('docker') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
          sh """
          docker build -f Dockerfile.test -t quorauk/testimage .
          """
          def image = docker.image("quorauk/testimage")
          image.push("latest")
        }
      }
    }
  }
}

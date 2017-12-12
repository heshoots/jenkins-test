podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "quorauk/testimage"
  node('docker') {
    stage('Build test image') {
      git 'https://github.com/heshoots/jenkins-test'
      container('docker') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
          sh """
          docker build -f Dockerfile.test -t ${image} .
          """
          def image = docker.image("quoruauk/testimage")
          image.push("latest")
        }
      }
    }
  }
}

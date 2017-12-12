podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "quorauk/testimage"
  node('docker') {
    stage('Build Docker image') {
      git 'https://github.com/heshoots/jenkins-test'
      container('docker') {
        sh "docker build -t ${image} ."
      }
    }
  }
}

podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "testimage"
  def registry = "registry-docker-registry:5000/"
  node('docker') {
    stage('Build test image') {
      git 'https://github.com/heshoots/jenkins-test'
      container('docker') {
        sh """
        docker build -f Dockerfile.test -t ${registry}/${image} .
        docker push ${registry}/${image}
        """
      }
    }
  }
}

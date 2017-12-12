podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:17.11.0-ce', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def imageName = "quorauk/testimage"
  node('docker') {
    container('docker') {
      // git 'https://github.com/heshoots/jenkins-test' ${GIT_LOCAL_BRANCH}
      stage('Build test image') {
        sh "docker build -f Dockerfile.test -t ${imageName} ."
      }
      stage('Test test image') {
        sh "docker run --rm ${imageName} sh -c 'npm run lint'"
      }
      stage('Build production image') {
        sh "docker build -f Dockerfile.prod -t ${imageName} ."
      }
      stage('Upload production image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
          def image = docker.image("quorauk/testimage")
          image.push("latest")
        }
      }
    }
  }
}

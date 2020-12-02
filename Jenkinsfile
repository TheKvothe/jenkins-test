pipeline {
  agent any
  environment{
    DOCKER_HOST = '192.168.194.130'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:${GIT_COMMIT} .'
      }
    }
  }
}

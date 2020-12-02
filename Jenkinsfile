pipeline {
  agent any
  environment{
  }
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:${GIT_COMMIT} .'
      }
    }
  }
}

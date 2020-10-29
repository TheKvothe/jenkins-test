pipeline {
  agent any
  environment{
    DOCKER_HOST = '192.168.194.130'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:${GIT_COMMIT} .'
        sh 'docker tag halloween-web:${GIT_COMMIT}  192.168.194.130:5000/halloween-docker:latest'
      }
    }

    stage('Push image to registry') {
      steps {
        sh 'docker push  192.168.194.130:5000/halloween-docker:latest'
      }
    }
    stage("redeploy"){
      steps {
        sh 'docker pull 192.168.194.130:5000/halloween-docker:latest'
        sh 'docker restart web-fest'
      }
    }
  }
}

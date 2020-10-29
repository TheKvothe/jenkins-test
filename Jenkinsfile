pipeline {
  agent any
  environment{
    DOCKER_HOST = '192.168.194.130'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:${GIT_COMMIT} .'
        sh 'docker tag halloween-web:${GIT_COMMIT}  192.168.194.130:5000/halloween-docker:${GIT_COMMIT}'
      }
    }

    stage('Push image to registry') {
      steps {
        sh 'docker push  192.168.194.130:5000/halloween-docker:${GIT_COMMIT}'
      }
    }
    stage("redeploy"){
      steps {
        sh 'docker stop web-fest'
        sh 'docker rm web-fest'
        sh 'docker pull 192.168.194.130:5000/halloween-docker:${GIT_COMMIT}'
        sh 'docker run --name web-fest -d -p 8080:80 192.168.194.130:5000/halloween-docker:${GIT_COMMIT}'
      }
    }
  }
}

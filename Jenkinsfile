pipeline {
  agent any
  environment{
    DOCKER_HOST = '192.168.194.130'
  }
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:${BUILD_NUMBER}:${TAG_NUMBER} .'
        sh 'docker tag halloween-web:${BUILD_NUMBER}:${TAG_NUMBER}  192.168.194.130:5000/halloween-docker:${TAG_NUMBER}'
      }
    }

    stage('Push image to registry') {
      steps {
        sh 'docker push  192.168.194.130:5000/halloween-docker:${TAG_NUMBER}'
      }
    }
    stage("redeploy"){
      steps {
        sh 'docker pull 192.168.194.130:5000/halloween-docker:${TAG_NUMBER}'
        sh 'docker run -d -p 8080:80 192.168.194.130:5000/halloween-docker:${TAG_NUMBER}'
      }
    }
  }
}

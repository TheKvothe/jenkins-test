pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t halloween-web:v1 . | grep built | cut -d " " -f3 > test.txt'
        sh 'docker tag $(cat test.txt) 192.168.194.130:5000/halloween-docker:v1'
      }
    }

    stage('Push image to registry') {
      steps {
        sh 'docker push  192.168.194.130:5000/halloween-docker:v1'
      }
    }

  }
}
pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('haythem22-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t haythem22/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push haythem22/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

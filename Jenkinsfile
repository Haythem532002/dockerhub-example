pipeline {
  agent any
  environment {
      DOCKER_IMAGE = "haythem22/dockerhub-example"
      IMAGE_TAG = "latest"
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t haythem22/dp-alpine:latest .'
      }
    }
    stage('Push to Docker Hub') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'haythem22-dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                sh "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
            }
        }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

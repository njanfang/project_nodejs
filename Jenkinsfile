
pipeline {
  agent any
  
  environment {
    // Define environment variables (if needed)
    DOCKER_REGISTRY = 'your-docker-registry-url' // Replace with your Docker registry URL
    IMAGE_NAME = 'node-app'
    IMAGE_TAG = 'latest'
  }
  
  stages {
    stage('Build Docker Image') {
      steps {
        // Build Docker image
        script {
          sh 'docker build -t $DOCKER_REGISTRY/$IMAGE_NAME:$IMAGE_TAG .'
        }
      }
    }

    stage('Push to Docker Registry') {
      steps {
        script {
          // Push Docker image to registry
          sh 'docker login -u <username> -p <password> $DOCKER_REGISTRY'
          sh 'docker push $DOCKER_REGISTRY/$IMAGE_NAME:$IMAGE_TAG'
        }
      }
    }
  }

  post {
    success {
      script {
        // Slack notification for successful build and push
        slackSend(channel: '#node_app', message: ':heavy_check_mark: Docker image build and push successful!')
      }
    }
    failure {
      script {
        // Slack notification for failed build or push
        slackSend(channel: '#node_app', message: ':x: Docker image build or push failed!')
      }
    }
  }
}
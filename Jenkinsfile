pipeline {
  agent any
  environment {
    DOCKER_IMAGE = "suhasini03/myapp-backend:v1"  // Replace with your DockerHub username
  }
  stages {
    stage('Checkout Code') {
      steps {
        git branch: 'master', url: 'https://github.com/Suhasiniphatak/Jenkinsfile.git'  // Replace with your repo URL
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $DOCKER_IMAGE .'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm install'
        sh 'npm test'
      }
    }
    stage('Scan with Trivy') {
      steps {
        sh 'trivy image $DOCKER_IMAGE'
      }
    }
    stage('Push Image to Docker Hub') {
      steps {
        withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
          sh 'docker push $DOCKER_IMAGE'
        }
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f k8s/deployment.yaml'
      }
    }
  }
}

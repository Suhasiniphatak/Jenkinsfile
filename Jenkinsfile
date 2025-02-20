pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "suhasini03/myapp-backend:v1"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'your-git-credentials-id', url: 'https://github.com/Suhasiniphatak/Jenkinsfile.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }
        stage('Scan with Trivy') {
            steps {
                bat 'trivy image $DOCKER_IMAGE'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'your-dockerhub-credentials-id', url: '']) {
                    bat 'docker push $DOCKER_IMAGE'
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

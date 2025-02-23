pipeline {
agent any
environment {
DOCKER_IMAGE = "suhasini03/myapp-backend:v1"
}
stages {
stage('Checkout Code') {
steps {
git branch:'main', url: 'https://github.com/Suhasiniphatak/Jenkinsfile.git'
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
stage('Pubat Image to Docker Hub') {
steps {
bat 'docker pubat $DOCKER_IMAGE'
}
}
stage('Deploy to Kubernetes') {
steps {
bat 'kubectl apply -f k8s/deployment.yaml'
}
}
}
}

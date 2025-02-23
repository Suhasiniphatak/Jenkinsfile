pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "suhasini03/myapp-backend:v1"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Suhasiniphatak/Jenkinsfile.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Run Tests') {
            steps {
                bat "npm install"  // Ensure dependencies are installed
                bat "npm test"     // Run tests
            }
        }

        stage('Scan with Trivy') {
            steps {
                bat "trivy image ${DOCKER_IMAGE}"
            }
        }

        stage('Push Image to Docker Hub') {  // Fixed stage name
            steps {
                bat "docker login -u suhasini03 -p Suhasini##03"
                bat "docker push ${DOCKER_IMAGE}"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl apply -f k8s/deployment.yaml --namespace=my-namespace"
            }
        }
    }
}

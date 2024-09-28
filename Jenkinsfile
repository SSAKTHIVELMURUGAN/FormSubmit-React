pipeline {
    agent any

    environment {
        // Define the Docker image name (your Docker Hub username)
        IMAGE_NAME = "sakthivelmurugan2003/form-react-app"
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the repository containing your React app
                git branch: 'main', url: 'https://github.com/SSAKTHIVELMURUGAN/FormSubmit-React.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the provided Dockerfile
                    def app = docker.build("$IMAGE_NAME:latest")
                }
            }
        }

        stage('Docker Hub Login') {
            steps {
                script {
                    // Login to Docker Hub using credentials stored in Jenkins
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        echo 'Logged into Docker Hub'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("$IMAGE_NAME:latest").push()
                    }
                }
            }
        }
    }
}

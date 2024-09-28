pipeline {
    agent any

    environment {
        // Replace these with your actual Docker Hub credentials stored in Jenkins
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
        DOCKER_HUB_REPO = 'yourdockerhubusername/react-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from your Git repository
                git 'https://github.com/yourusername/your-repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Use npm to install dependencies
                    bat 'npm install'
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    // Build the React application
                    bat 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    bat 'docker build -t %DOCKER_HUB_REPO%:latest .'
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    bat 'echo %DOCKER_HUB_CREDENTIALS_PSW% | docker login -u %DOCKER_HUB_CREDENTIALS_USR% --password-stdin'

                    // Push the Docker image
                    bat 'docker push %DOCKER_HUB_REPO%:latest'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
    }
}

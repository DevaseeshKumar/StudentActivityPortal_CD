pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('Jenkins-Docker') // Optional: for Docker Hub auth
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/DevaseeshKumar/StudentActivityPortal_CDD.git'
            }
        }

        stage('Build Maven Package') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Start Services with Docker Compose') {
            steps {
                script {
                    bat 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
        cleanup {
            cleanWs() // only cleans Jenkins workspace, not containers
        }
    }
}

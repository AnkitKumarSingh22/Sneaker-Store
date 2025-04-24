pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token')
        IMAGE_NAME = 'sneaker-store-frontend'
        CONTAINER_NAME = 'my-frontend-container'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/AnkitKumarSingh22/Sneaker-Store', credentialsId: 'github-token'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Stop Existing Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Run Updated Container') {
            steps {
                script {
                    sh "docker run -d --name ${CONTAINER_NAME} -p 8081:80 ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Website deployed on localhost:8081 as my-frontend-container'
        }
        failure {
            echo '❌ Build or deployment failed.'
        }
    }
}

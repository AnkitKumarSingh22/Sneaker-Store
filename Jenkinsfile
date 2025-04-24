pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token')
        IMAGE_NAME = 'sneaker-store-frontend'
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

        stage('Stop Existing Containers') {
            steps {
                script {
                    sh '''
                        docker rm -f sneaker-store-8081 || true
                        docker rm -f sneaker-store-8085 || true
                    '''
                }
            }
        }

        stage('Run Container on Port 8081') {
            steps {
                script {
                    sh "docker run -d --name sneaker-store-8081 -p 8081:80 ${IMAGE_NAME}"
                }
            }
        }

        stage('Run Container on Port 8085') {
            steps {
                script {
                    sh "docker run -d --name sneaker-store-8085 -p 8085:8080 ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Website deployed successfully on ports 8081 and 8085!'
        }
        failure {
            echo '❌ Build or deployment failed.'
        }
    }
}

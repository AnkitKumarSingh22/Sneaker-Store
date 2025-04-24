pipeline {
agent any

environment {
    GITHUB_TOKEN = credentials('github-token')
}

stages {
    stage('Checkout') {
        steps {
            git url: 'https://github.com/AnkitKumarSingh22/Sneaker-Store', credentialsId: 'github-token'
        }
    }

    stage('Build Docker Image') {
        steps {
            script {
                sh 'docker build -t sneaker-store-frontend .'
            }
        }
    }

    stage('Run Docker Image') {
        steps {
            script {
                sh 'docker run -d -p 8081:8080 sneaker-store-frontend'
            }
        }
    }
}

post {
    success {
        echo 'Build and deployment succeeded!'
    }
    failure {
        echo 'Build or deployment failed!'
    }
}
}
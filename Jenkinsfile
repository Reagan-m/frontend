pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/Reagan-m/frontend.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t frontend-app:1 .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop frontend-container || true'
                sh 'docker rm frontend-container || true'
                sh 'docker run -d -p 80:80 --name frontend-container frontend-app:1'
            }
        }
    }
}



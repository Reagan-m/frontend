pipeline {
    agent any

    environment {
        IMAGE_NAME = "frontend-app"
        CONTAINER_NAME = "frontend-container"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/Reagan-m/frontend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                if [ "$(docker ps -q -f name=$CONTAINER_NAME)" ]; then
                    docker stop $CONTAINER_NAME
                    docker rm $CONTAINER_NAME
                fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}

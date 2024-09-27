pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'mohamedessam1911/simple-web-app'
        DOCKER_CREDENTIALS_ID = 'Dockerhub'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                    docker build -t ${DOCKER_HUB_REPO}:latest .
                    """
                }
            }
        }
        stage('Docker Login') {
            steps {
                script {
                    sh """
                    echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin
                    """
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh """
                    docker push ${DOCKER_HUB_REPO}:latest
                    """
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh """
                    docker run -d -p 3000:3000 --name simple-web-app ${DOCKER_HUB_REPO}:latest
                    """
                }
            }
        }
    }
}

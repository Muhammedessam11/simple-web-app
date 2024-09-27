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
                    dockerImage = docker.build(DOCKER_HUB_REPO)
                }
            }
        }
        stage('Docker Login') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        // Perform the Docker login
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        dockerImage.push('latest')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 --name simple-web-app ${DOCKER_HUB_REPO}:latest'
                }
            }
        }
    }
}

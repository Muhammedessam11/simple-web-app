pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('Dockerhub')
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t mohamedessam1911/simple-web-app:latest .'
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    sh '''
                        echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push mohamedessam1911/simple-web-app:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh '''
                        cd /path/to/deployment/directory  # Replace with your deployment path
                        docker pull mohamedessam1911/simple-web-app:latest
                        docker stop web-app || true
                        docker rm web-app || true
                        docker run -d -p 3000:3000 --name web-app mohamedessam1911/simple-web-app:latest
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

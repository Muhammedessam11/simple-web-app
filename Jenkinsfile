pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'mohamedessam1911/simple-web-app'
        DOCKERHUB_CREDENTIALS=credentials('Dockerhub')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_HUB_REPO)
                }
            }
        }
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push Docker Image') {
            steps {
                docker.image(DOCKER_HUB_REPO).push('latest')
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

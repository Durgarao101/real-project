pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "durga83125/durga83125"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout the code from Github Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Durgarao101/real-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker Image: ${DOCKER_HUB_REPO}:${IMAGE_TAG}"
                    dockerImage = docker.build("${DOCKER_HUB_REPO}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}

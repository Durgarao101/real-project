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
                    echo "Building Docker Image: ${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}"
                    def app = docker.build("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    docker.withRegistry("https://index.docker.io/v1/", "dockerhub-credentials") {
                        def app = docker.image("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}")
                        app.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check logs."
        }
    }
}


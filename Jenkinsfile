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

                    // Store docker image globally
                    env.IMAGE_NAME = "${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}"
                    app = docker.build(env.IMAGE_NAME)
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."

                    docker.withRegistry("https://index.docker.io/v1/", "dockerhub-credentials") {
                        app.push()   // now this works
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

pipeline{
    agent any
    environment{
        DOCKER_HUB_REPO="durga83125/durga83125"
        IMAGE_TAG="lastest"
    }
    stages{
        stage('Checkout the code from Github Repository'){
            steps{
                https://github.com/Durgarao101/real-project.git
            }
        }
        stage('Bulid Docker Image'){
            steps{
                echo "Building Docker Image: ${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}"
                    docker.build("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}").push()
                    }
                }
            }
        }
    }


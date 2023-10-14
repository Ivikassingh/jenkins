pipeline {
    agent any

    environment {
        // Set the Docker image name
        DOCKER_IMAGE_NAME = 'my-python-app'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Assuming you're using a Git SCM source
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                }
            }
        }

        // Optional: Push the image to a registry
        stage('Push Docker Image') {
            steps {
                script {
                    // Assuming you've logged into DockerHub or another registry already
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerHubCredentials') {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'Job succeeded!'
        }
        failure {
            echo 'Job failed!'
        }
    }
}
pipeline {
    agent any

    environment {
        // Set the Docker image name
        DOCKER_IMAGE_NAME = 'viiky/jenkins'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Assuming you're using a Git SCM source
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                }
            }
        }

        // Optional: Push the image to a registry
        stage('Push Docker Image') {
            steps {
                script {
                    // Assuming you've logged into DockerHub or another registry already
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerHubCredentials') {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'Job succeeded!'
        }
        failure {
            echo 'Job failed!'
        }
    }
}

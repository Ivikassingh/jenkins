
pipeline {
    agent any

    environment {
        // Set the Docker image name
        DOCKER_IMAGE_NAME = 'viiky/jenkins'
        DOCKER_IMAGE_TAG = 'latest'
        EC2_IP = '54.236.30.253'
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

        stage('Deploy Docker Image to EC2') {
            steps {
                script {
                    // SSH into the EC2 instance
                    sshagent(credentials:['sshec2']) {
                        sh '''
                            ssh -o StrictHostKeyChecking=no ec2-user@EC2_IP "docker pull DOCKER_IMAGE_NAME:DOCKER_IMAGE_TAG"
                            ssh -o StrictHostKeyChecking=no ec2-user@EC2_IP "docker run -d -p 80:80 DOCKER_IMAGE_NAME:DOCKER_IMAGE_TAG"
                        '''
                    }
                }
            }
        }
    }

}

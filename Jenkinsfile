pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "python-1"
        DOCKER_CONTAINER_NAME = "python-1" 
        GIT_REPO = "https://github.com/navy77/jenkins-python.git" 
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh """
                    docker stop ${DOCKER_CONTAINER_NAME} || true
                    docker rm ${DOCKER_CONTAINER_NAME} || true
                    docker run -d --name ${DOCKER_CONTAINER_NAME} ${DOCKER_IMAGE_NAME}
                    """
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}


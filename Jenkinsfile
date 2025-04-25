pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "python-1"
        DOCKER_CONTAINER_NAME = "python-1" 
        GIT_REPO = "https://github.com/navy77/jenkins-python.git" 
        GIT_TAG = ""
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'production', url: "${GIT_REPO}"
            }
        }

        stage('Get Git Tag') {
            steps {
                script {
                    GIT_TAG = sh(script: 'git describe --tags --exact-match || echo "no-tag"', returnStdout: true).trim()
                    if (GIT_TAG == "no-tag") {
                        error("No Git tag found on this commit!")
                    }
                    echo "Using Git Tag: ${GIT_TAG}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${GIT_TAG} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh """
                    docker stop ${DOCKER_CONTAINER_NAME} || true
                    docker rm ${DOCKER_CONTAINER_NAME} || true
                    docker run -d --name ${DOCKER_CONTAINER_NAME} ${DOCKER_IMAGE_NAME}:${GIT_TAG}
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
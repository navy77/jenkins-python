pipeline {
    environment {
        imagename = "python/app"
    }
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/navy77/jenkins-python.git', branch: 'main'
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Running tests..."
                # Replace this with actual test commands
                echo "Tests passed!"
                '''
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'python:3.12-alpine'
                }
            }
            steps {
                sh '''
                echo "Building Docker image..."
                docker build -t python/app .
                '''
            }
        }
    }
}

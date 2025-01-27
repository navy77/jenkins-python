pipeline {
    environment {
        image_name = "python/app"
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
                '''
            }
        }

        stage('Build images') {
            steps{
                sh '''
                ls -la
                docker build -t python-app .
                docker run -d --name python python-app:latest
                '''
            }
            }
        }
    }


pipeline {
    environment {
    imagename = "python/app"
    dockerImage = ''
  }
    agent any

    stages {
        stage('Clone respository') {
            steps {
                git([url: 'https://github.com/navy77/jenkins-python.git', branch: 'main'])
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo 'my-python jenkins !'
                '''
            }
        }

        // stage('Approval') {
        //     steps {
        //         timeout(time: 180, unit: 'SECONDS') {
        //             input message: 'Do you wish to deploy tp production ?', ok: 'Yes ,I am sure!'
        //     }
        //         }
        // }

        stage('Build') {
            agent {
                docker {
                    image 'python:3.12-alpine'
                }
            }
            steps {
                    sh 'docker build -t python-app .'
                    // dockerImage = docker.build imagename
            }
        }


    }
}
pipeline {
    agent any

    stages {
        stage('cClone respository') {
            checout scm
        }

        stage('Test') {
            steps {
                sh '''
                echo 'my-python jenkins !'
                ls -la
                '''
            }
        }

        stage('Approval') {
            steps {
                timeout(time: 180, unit: 'SECONDS') {
                    input message: 'Do you wish to deploy tp production ?', ok: 'Yes ,I am sure!'
            }
                }
        }

        stage('Build') {
            agent {
                docker {
                    image 'python:3.12-alpine'
                }
            }
            steps {
                    sh 'docker build -t python-app .'
            }
        }


    }
}
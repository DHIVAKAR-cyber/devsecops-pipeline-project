
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace.'
                sh 'git --version'
            }
        }

        stage('Docker Check') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Application Check') {
            steps {
                sh 'test -f app/manage.py'
                echo 'Django application file found.'
            }
        }
    }
}

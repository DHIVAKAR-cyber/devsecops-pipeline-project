pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh 'git --version'
                sh 'docker --version'
                sh 'docker compose version'
            }
        }

        stage('Verify Application') {
            steps {
                sh 'test -f app/manage.py'
                sh 'test -f app/Dockerfile'
                echo 'Application files verified.'
            }
        }

        stage('Test Application') {
            steps {
                sh 'docker compose -f docker-compose.yml -f compose.test.yaml run --build --rm web python manage.py test hospital'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-django-app:jenkins -f app/Dockerfile app'
            }
        }
    }

    post {
        always {
            sh 'docker compose down --remove-orphans'
        }
    }
}

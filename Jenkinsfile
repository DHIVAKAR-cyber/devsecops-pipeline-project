
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
            }
        }

        stage('Verify Application') {
            steps {
                sh 'test -f app/manage.py'
                sh 'test -f app/Dockerfile'
                echo 'Application files verified.'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-django-app:jenkins -f app/Dockerfile app'
            }
        }
    }
}

stage('Test Application') {
    steps {
        sh 'docker compose run --build --rm web python manage.py test hospital'
    }
}
post {
    always {
        sh 'docker compose down --remove-orphans'
    }
}

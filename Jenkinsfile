pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "afrimart"
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh 'echo "Checking Git..."'
                sh 'git --version'

                sh 'echo "Checking Docker..."'
                sh 'docker --version'

                sh 'echo "Checking Docker Compose..."'
                sh 'docker compose version'

                sh 'echo "Checking Buildx..."'
                sh 'docker buildx version || true'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose build --no-cache'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Show Running Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo '✅ Afrimart deployment successful!'
        }
        failure {
            echo '❌ Build failed. Check logs above.'
        }
    }
}

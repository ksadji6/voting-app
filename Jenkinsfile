pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ksadji6/voting-app.git', branch: 'main'
                echo 'Source code checked out successfully.'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    echo 'Building Docker images for all services...'
                    sh 'docker compose build --no-cache'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    echo 'Deploying the application stack...'
                    sh 'docker compose up -d'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    echo 'Verifying the status of deployed services...'
                    sh 'docker compose ps'
                    sleep(time: 10, unit: 'SECONDS')
                    echo 'Deployment verification complete.'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. Cleaning up workspace.'
        }
    }
}

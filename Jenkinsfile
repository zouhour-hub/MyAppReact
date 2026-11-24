pipeline {
    agent any

    stages {
        stage('Build Images') {
            steps {
                bat 'docker build -t mern-server ./Server'
                bat 'docker build -t mern-client ./Client'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                bat script: 'docker compose down --remove-orphans', returnStatus: true
                bat 'docker compose up -d --build'
            }
        }

        stage('Verify') {
            steps {
                bat 'docker compose ps'
            }
        }
    }

    post {
        always {
            bat script: 'docker image prune -f', returnStatus: true
        }
        failure {
            bat script: 'docker compose logs --tail=50', returnStatus: true
        }
    }
}

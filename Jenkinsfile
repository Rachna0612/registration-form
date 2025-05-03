pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy with Docker Compose') {
            steps {
                script {
                    // Stop any running containers (if any)
                    sh 'docker-compose down || true'
                    // Build and start Nginx with your static files
                    sh 'docker-compose up -d --build'
                }
            }
        }
        stage('Health Check') {
            steps {
                // Check that the main page is served
                sh 'curl --fail http://localhost:8080/index.html'
            }
        }
    }
    post {
        always {
            // Clean up containers after the pipeline (optional)
            sh 'docker-compose down'
        }
    }
}

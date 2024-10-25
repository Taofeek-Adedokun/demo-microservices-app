pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials' // Your credential ID
    }

    stages {
        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build("Neyomr47/frontend:latest", "./frontend")
                }
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    docker.build("Neyomr47/backend:latest", "./backend")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Run Docker containers on Jenkins' Docker daemon
                    sh 'docker run -d -p 80:80 Neyomr47/frontend:latest'
                    sh 'docker run -d -p 3000:3000 Neyomr47/backend:latest'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker system prune -f' // Clean up unused Docker resources
            }
        }
    }
}


pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jagan-web:latest .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh '''
                    docker rm -f jagan-web || true
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker run -d \
                    --name jagan-web \
                    -p 8085:80 \
                    jagan-web:latest
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}

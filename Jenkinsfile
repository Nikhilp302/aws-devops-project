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
                sh 'docker build -t aws-devops-app:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop app || true
                docker rm app || true

                docker run -d \
                --name app \
                -p 80:5000 \
                aws-devops-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}


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
                sh 'docker build -t devops-webapp:latest .'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker rm -f devops-webapp || true
                    docker run -d --name devops-webapp -p 80:80 devops-webapp:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl -f http://localhost/'
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 --version'
                sh 'pip3 --version'
                sh 'pip3 install -r requirements.txt --user'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t simple-app:latest ."
            }
        }

        stage('Run Container') {
            steps {
                sh "docker stop simple-app || true"
                sh "docker rm simple-app || true"
                sh "docker run -d --name simple-app -p 5000:5000 simple-app:latest"
            }
        }
    }
}
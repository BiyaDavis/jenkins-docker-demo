pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            agent { docker { image 'python:3.10' } }
            steps {
                sh 'pip install -r requirements.txt'
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

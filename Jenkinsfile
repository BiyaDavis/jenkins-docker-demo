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

                sh '''
                if command -v pip3 >/dev/null 2>&1; then
                    echo "Using pip3"
                    pip3 install -r requirements.txt --break-system-packages
                else
                    echo "pip3 not found, using pip"
                    pip install -r requirements.txt --break-system-packages
                fi
                '''
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
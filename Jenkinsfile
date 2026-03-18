pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                echo 'Proyecto clonado correctamente desde GitHub'
            }
        }
        
        stage('Test') {
            steps {
                sh '''
                    docker run --rm -v ${WORKSPACE}:/app -w /app python:3.9-slim python -m pip install flask pytest
                    docker run --rm -v ${WORKSPACE}:/app -w /app python:3.9-slim python -m pytest test_app.py
                '''
            }
        }
        
        stage('Build Image') {
            steps {
                sh 'docker build -t anisasaguer/python-app:latest .'
            }
        }
        
        stage('DockerHub') {
            steps {
                sh 'docker push anisasaguer/python-app:latest'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}

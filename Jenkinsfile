pipeline {
    agent {
        docker {
            image 'python:3.9-slim'
        }
    }
    stages {
        stage('Clone') {
            steps {
                echo 'Proyecto clonado correctamente desde GitHub'
            }
        }
        stage('Test') {
            steps {
                sh 'pip install flask pytest'
                sh 'pytest test_app.py'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    def dockerImage = "anisasaguerallouseso/python-app:latest"
                    sh "docker build -t ${dockerImage} ."
                }
            }
        }
        stage('DockerHub') {
            steps {
                script {
                    def dockerImage = "anisasaguerallouseso/python-app:latest"
                    sh "docker push ${dockerImage}"
                }
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

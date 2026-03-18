pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                echo 'Proyecto clonado correctamente'
            }
        }
        
        stage('Test') {
            steps {
                sh 'pip3 install --break-system-packages flask pytest'
                sh 'python3 -m pytest test_app.py'
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
                echo 'Despliegue manual: ejecutar kubectl desde la terminal'
                sh 'cp deployment.yaml /tmp/deployment.yaml'
                sh 'cp service.yaml /tmp/service.yaml'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completado. Para desplegar, ejecuta:'
            echo 'kubectl apply -f /tmp/deployment.yaml'
            echo 'kubectl apply -f /tmp/service.yaml'
        }
    }
}

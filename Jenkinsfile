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
        sh '''
            kubectl --server=https://192.168.49.2:8443 \
                    --insecure-skip-tls-verify=true \
                    --kubeconfig=/dev/null \
                    apply -f deployment.yaml
            kubectl --server=https://192.168.49.2:8443 \
                    --insecure-skip-tls-verify=true \
                    --kubeconfig=/dev/null \
                    apply -f service.yaml
        '''
            }
        }
    }
}

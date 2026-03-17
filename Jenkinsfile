stage('Test') {
    steps {
        script {
            sh '''
                docker run --rm -v $(pwd):/app -w /app python:3.9-slim \
                    bash -c "pip install flask pytest && pytest test_app.py"
            '''
        }
    }
}

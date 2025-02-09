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
                script {
                    docker.build("mon-app-react:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    sh """
                        docker stop mon-app-react || true
                        docker rm mon-app-react || true
                        docker run -d -p 80:80 --name mon-app-react mon-app-react:${BUILD_NUMBER}
                    """
                }
            }
        }
    }
}
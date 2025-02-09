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
                    bat 'docker build --no-cache -t mon-app-react .'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    bat '''
                        docker stop mon-app-react || exit 0
                        docker rm mon-app-react || exit 0
                    '''
                    bat 'docker run -d -p 80:80 --name mon-app-react mon-app-react'
                }
            }
        }
    }

    post {
        always {
            bat 'docker image prune -f'
        }
    }
}
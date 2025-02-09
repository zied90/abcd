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
                    // Utilisation de --no-cache pour forcer un nouveau build
                    sh 'docker build --no-cache -t mon-app-react .'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Arrêt et suppression du container existant s'il existe
                    sh '''
                        docker stop mon-app-react || true
                        docker rm mon-app-react || true
                    '''
                    
                    // Démarrage du nouveau container
                    sh 'docker run -d -p 80:80 --name mon-app-react mon-app-react'
                }
            }
        }
    }

    // Nettoyage après le build
    post {
        always {
            // Nettoyage des images non utilisées
            sh 'docker image prune -f'
        }
    }
}
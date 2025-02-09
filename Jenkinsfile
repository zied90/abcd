pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/zied90/abcd.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }
        stage('Docker Build & Run') {
            steps {
                bat '''
                docker build -t mon-app-react .
                docker stop mon-app-react || true
                docker rm mon-app-react || true
                docker run -d --name mon-app-react -p 80:80 mon-app-react
                '''
            }
        }
    }
}

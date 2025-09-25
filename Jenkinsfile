pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dilkkumar/flask_app'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t flask-app-ci .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm flask-app-ci pytest tests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                docker run -d --name flask-container -p 5000:5000 flask-app-ci
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build, Test, Deploy Successful!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}

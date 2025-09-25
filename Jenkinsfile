pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: '<your-github-repo-link>'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t flask-app-ci .'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest tests'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 flask-app-ci'
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

pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo 'Source code is available in Jenkins workspace'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ci-cd-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop ci-cd-container || true'
                sh 'docker rm ci-cd-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name ci-cd-container ci-cd-app'
            }
        }
    }

    post {
        success {
            echo 'Application Deployed Successfully!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}

pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/nani-804/autonomous-release-orchestration-platform.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'cd app && docker build -t release-app:${BUILD_NUMBER} .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh 'docker images'
            }
        }

    }
}

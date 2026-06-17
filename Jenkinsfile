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

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f release-container || true

                docker run -d \
                --name release-container \
                -p 5000:5000 \
                release-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Health Check') {
    steps {
        sh '''
        sleep 10
        curl localhost:5000
        '''
            }
        }
    }
}

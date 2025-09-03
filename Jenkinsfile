pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ScileValence/youtube-clone.git',
                    credentialsId: 'github-creds'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("youtube-clone:${BUILD_NUMBER}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop old container if running
                    sh 'docker rm -f youtube-clone || true'

                    // Run new container on port 9090 (since Jenkins uses 8080)
                    sh "docker run -d -p 9090:80 --name youtube-clone youtube-clone:${BUILD_NUMBER}"
                }
            }
        }
    }
}

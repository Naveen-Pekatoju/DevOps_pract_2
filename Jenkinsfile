pipeline {
    agent any

    environment {
        IMAGE_NAME = "calculator-app"
        DOCKERHUB_USER = "YOUR_USERNAME"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/YOUR_USERNAME/calculator-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_USER}/${IMAGE_NAME}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 ${DOCKERHUB_USER}/${IMAGE_NAME}'
                }
            }
        }
    }
}

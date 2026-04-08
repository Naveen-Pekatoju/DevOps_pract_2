pipeline {
    agent any

    environment {
        IMAGE_NAME = "naveenpekatoju/calculator"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t calculator-app:${BUILD_NUMBER} .
                docker tag calculator-app:${BUILD_NUMBER} ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker stop calculator-container || true
                docker rm calculator-container || true
                docker run -d -p 3000:3000 --name calculator-container ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }
}

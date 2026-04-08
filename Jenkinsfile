pipeline {
    agent any

    environment {
        IMAGE_NAME = "calculator-app"
        DOCKERHUB_USER = "naveenpekatoju"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t reg-app:${BUILD_NUMBER} .
                docker tag reg-app:${BUILD_NUMBER} ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop calculator-container || true
                docker rm calculator-container || true
                docker run -d -p 3000:3000 --name calculator-container ${DOCKERHUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }
}

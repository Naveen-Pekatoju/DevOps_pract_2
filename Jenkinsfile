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
                docker tag reg-app:${BUILD_NUMBER} $IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }


        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
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

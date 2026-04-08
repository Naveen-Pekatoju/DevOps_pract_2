pipeline {
    agent any

    environment {
        IMAGE_NAME = "calculator-app"
        DOCKERHUB_USER = "naveenpekatoju"
    }

    stages {

        

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

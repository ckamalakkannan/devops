pipeline {
    agent any

    environment {
        IMAGE_NAME = "kamaltest"
        CONTAINER_NAME = "kamaltestcn"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ckamalakkannan/devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Stop Previous Container') {
            steps {
                script {
                    sh """
                    docker rm -f ${CONTAINER_NAME} || true
                    """
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh """
                    docker run -d --name ${CONTAINER_NAME} -p 8888:80 ${IMAGE_NAME}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Webpage deployed successfully! Visit http://localhost:8888"
        }
        failure {
            echo "Build failed. Check logs for errors."
        }
    }
}

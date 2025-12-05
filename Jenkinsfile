pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds')
        IMAGE_NAME = "rakesh612/python-app"   // <-- Change to your Docker Hub repo
    }

    stages {

        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/chauhan46/Python-app.git'
            }
        }

        stage("Build Docker Image") {
            steps {
                sh """
                echo Building Docker Image...
                docker build -t ${IMAGE_NAME}:latest .
                """
            }
        }

        stage("Login to Docker Hub") {
            steps {
                sh """
                echo Logging in to Docker Hub...
                echo "${DOCKERHUB_CREDENTIALS_PSW}" | docker login -u "${DOCKERHUB_CREDENTIALS_USR}" --password-stdin
                """
            }
        }

        stage("Push Docker Image") {
            steps {
                sh """
                echo Pushing Image...
                docker push ${IMAGE_NAME}:latest
                """
            }
        }
    }

    post {
        always {
            echo "Pipeline finished!"
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds')
        IMAGE_NAME = "your-image-name"
    }

    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/chauhan46/Python-app.git'
            }
        }

        stage("Build") {
            steps {
                sh 'echo Building...'
            }
        }
    }

    post {
        always {
            script {
                echo "Pipeline finished!"

                // ✔ Wrap post actions inside node if you use sh
                node {
                    sh "echo Cleanup step running..."
                }
            }
        }
    }
}



pipeline {
    agent any

    environment {
        IMAGE_NAME = "simple-php-app"
        IMAGE_TAG = "${env.BUILD_NUMBER}"
        CONTAINER_NAME = "php-container"
        HOST_PORT = "8081"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                bat "docker stop %CONTAINER_NAME% || echo No running container"
                bat "docker rm %CONTAINER_NAME% || echo No container to remove"
            }
        }

        stage('Run New Container') {
            steps {
                bat "docker run -d -p %HOST_PORT%:80 --name %CONTAINER_NAME% %IMAGE_NAME%:%IMAGE_TAG%"
            }
        }

    }

    post {
        success {
            echo "Application successfully deployed at http://localhost:${HOST_PORT}"
        }
        failure {
            echo "Build failed. Check logs."
        }
        always {
            echo "Pipeline execution completed."
        }
    }
}

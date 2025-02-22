pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-sum-api"
        CONTAINER_NAME = "flask-test-container"
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker run -d --rm --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                    sleep 5  // Đợi container khởi động
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}") {
                        sh "docker exec ${CONTAINER_NAME} python -m unittest test_app.py"
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh "docker stop ${CONTAINER_NAME}"
                }
            }
        }
    }
}

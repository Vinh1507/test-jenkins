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

        stage('Run Tests') {
            steps {
                script {
                    sh "docker run --rm ${IMAGE_NAME} python -m unittest discover -s /app -p 'test_*.py'"
                }
            }
        }


        // stage('Cleanup') {
        //     steps {
        //         script {
        //             sh "docker stop ${CONTAINER_NAME}"
        //         }
        //     }
        // }
    }
}

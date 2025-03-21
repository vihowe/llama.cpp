pipeline {
    agent any  // Run on any available agent

    environment {
        IMAGE_NAME = "jenkins/llama.cpp:test"  // Define the image name
        DOCKERFILE_PATH = "./.devops/cpu.Dockerfile"  // Path to the Dockerfile
    }

    stages {
//        stage('Checkout Code') {
//            steps {
//                checkout scm  // Fetch the latest code from the repo
//            }
//        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} --target light -f ${DOCKERFILE_PATH} ."
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh "docker run --rm ${IMAGE_NAME} -h"
                }
            }
        }
    }

    post {
        always {
            script {
                sh "docker rmi ${IMAGE_NAME} || true"  // Clean up the image after execution
            }
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = 'nethmipoornima'
        IMAGE_TAG = '1.0.0'
    }

    stages {
        stage('Pull Git Repository') {
            steps {
                git branch: 'gscomp339', credentialsId: 'github-path-nethmi', url: 'https://github.com/NethmiAththanayaka/NCC_2025.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build Backend Image
                    sh "docker build -t ${DOCKERHUB_USERNAME}/backend2-app:${IMAGE_TAG} ./backend2"
                    // Build Frontend Image
                    sh "docker build -t ${DOCKERHUB_USERNAME}/frontend2-app:${IMAGE_TAG} ./frontend2"
                }
            }
        }

        stage('Push Docker Images to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-nethmipoornima', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker push ${DOCKERHUB_USERNAME}/backend2-app:${IMAGE_TAG}"
                        sh "docker push ${DOCKERHUB_USERNAME}/frontend2-app:${IMAGE_TAG}"
                        sh "docker logout"
                    }
                }
            }
        }
    }
}

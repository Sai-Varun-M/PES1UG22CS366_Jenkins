pipeline {
    agent {
        docker {
            image 'node:14'
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sai-Varun-M/PES1UG22CS366_Jenkins'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test application') {
            steps {
                sh 'npm test'
            }
        }
        stage('Push Docker image') {
            environment {
                DOCKER_USER = 'your-docker-username'  // Replace with your DockerHub username
                IMAGE_NAME = 'your-image-name'       // Replace with your Docker image name
            }
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker build -t $DOCKER_USER/$IMAGE_NAME:$BUILD_NUMBER .'
                    sh 'docker push $DOCKER_USER/$IMAGE_NAME:$BUILD_NUMBER'
                }
            }
        }
    }
}

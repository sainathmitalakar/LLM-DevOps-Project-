pipeline {
    agent any

    environment {
        IMAGE_NAME = "llm-devops"
        DOCKER_REGISTRY = "sainathmitalakar"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sainathmitalakar/llm-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $DOCKER_REGISTRY/$IMAGE_NAME:latest ."
                }
            }
        }

        stage('Push Image to Registry') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                        sh "echo $DOCKER_TOKEN | docker login -u $DOCKER_REGISTRY --password-stdin"
                        sh "docker push $DOCKER_REGISTRY/$IMAGE_NAME:latest"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh "kubectl apply -f k8s/deployment.yaml"
                sh "kubectl apply -f k8s/service.yaml"
            }
        }
    }
}

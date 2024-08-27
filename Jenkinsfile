pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ammar44555/nodejs.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building the project...'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Docker image build karna aur tag set karna
                    dockerImage = docker.build("ammar55/simple-nodejs:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Docker Hub ke registry ke saath authenticate karna aur image push karna
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        // Tag specify karna
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Kubernetes ko deploy karna
                sh 'kubectl apply -f kubernetes/deployment.yaml'
            }
        }
    }
}


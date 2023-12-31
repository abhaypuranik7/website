pipeline {
  
    agent {
        label 'node'
    }

  environment {
        IMAGE_NAME = 'abhaypuranik7/website:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                script {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying to Kubernetes...'
                script {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}

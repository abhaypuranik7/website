pipeline {
  
    agent {
        label 'node'
    }

  environment {
        IMAGE_NAME = 'abhaypuranik7/website:latest'
    }

    stages {
        stage('Delete Old Docker Image') {
            steps {
                echo 'Deleting old Docker image...'
                script {
                    sh 'docker ps -a -q --filter "ancestor=$IMAGE_NAME" | xargs -r docker stop'
                    sh 'docker ps -a -q --filter "ancestor=$IMAGE_NAME" | xargs -r docker rm'
                    sh 'docker rmi $IMAGE_NAME'
                }
            }
        }


        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                script {
                    sh 'sudo docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                script {
                    sh 'sudo docker push $IMAGE_NAME'
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

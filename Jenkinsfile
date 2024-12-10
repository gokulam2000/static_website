pipeline {
    agent any
    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo 'Pulling the Docker image...'
                    sh 'docker pull nginx:latest'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    echo 'Running the Docker container...'
                    sh '''
                        docker run -d --name my-nginx -p 8080:80 nginx:latest
                    '''
                }
            }
        }
        stage('Verify Container') {
            steps {
                script {
                    echo 'Checking if the container is running...'
                    sh 'docker ps | grep my-nginx'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            sh '''
                docker stop my-nginx || true
                docker rm my-nginx || true
            '''
        }
    }
}

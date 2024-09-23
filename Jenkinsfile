pipeline {
    agent any
    environment {
        DOCKER_HOST = "tcp://dind:2375"  // Use Docker daemon from the DinD container
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Starting dependency installation...'
                sh 'npm install --save'
                echo 'Dependencies installed successfully.'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    // Build the Docker image for the Node.js app using the Docker daemon in DinD
                    sh 'docker build -t my-node-app:latest .'
                }
                echo 'Docker image built successfully.'
            }
        }
        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    // Run the Docker container using the Docker daemon from DinD
                    sh 'docker run -d -p 3000:3000 --name my-node-app my-node-app:latest'
                }
                echo 'Docker container deployed successfully.'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
            script {
                sh 'docker ps -a'
                sh 'docker images'
            }
        }
    }
}

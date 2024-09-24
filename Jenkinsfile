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
                    // Build the Docker image for the Node.js app
                    sh 'docker build -t my-node-app:latest .'
                }
                echo 'Docker image built successfully.'
            }
        }
        stage('Run Docker Container') {
            steps {
                echo 'Checking if Docker container exists...'
                script {
                    // Check if the container is already running
                    def containerExists = sh(script: "docker ps -aq -f name=my-node-app", returnStdout: true).trim()
                    def containerRunning = sh(script: "docker ps -q -f name=my-node-app", returnStdout: true).trim()

                    if (containerExists && !containerRunning) {
                        // Container exists but is not running, so start it
                        echo "Starting existing container..."
                        sh 'docker start my-node-app'
                    } else if (!containerExists) {
                        // Container does not exist, so create and run a new one
                        echo "Creating and running a new container..."
                        sh 'docker run -d -p 3000:3000 --name my-node-app my-node-app:latest'
                    } else {
                        echo "Container is already running."
                    }
                }
                echo 'Docker container is up and running.'
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

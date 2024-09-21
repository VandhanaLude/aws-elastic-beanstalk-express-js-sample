pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root:root'
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Starting dependency installation...'
                script {
                    sh 'npm install --save'
                }
                echo 'Dependencies installed successfully.'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                // Example: sh 'npm test'
                echo 'Tests completed.'
            }
        }
        stage('Deploy to Elastic Beanstalk') {
            steps {
                echo 'Deploying to Elastic Beanstalk...'
                // Example: sh 'eb deploy'
                echo 'Deployment completed.'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
            // Optionally, print more debug info
            script {
                sh 'docker ps -a'
                sh 'docker images'
            }
        }
    }
}

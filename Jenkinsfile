pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
            script {
                bat 'curl -X POST "http://host.docker.internal:8081/api/jenkins-logs/webhook?jobName=stocksens&buildNumber=%BUILD_NUMBER%&buildStatus=SUCCESS&token=test"'
            }
        }

        failure {
            echo '❌ Build failed!'
            script {
                bat 'curl -X POST "http://host.docker.internal:8081/api/jenkins-logs/webhook?jobName=stocksens&buildNumber=%BUILD_NUMBER%&buildStatus=FAILURE&token=test"'
            }
        }
    }
}

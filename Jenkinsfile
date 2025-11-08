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
                // Tes étapes de build ici
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Tes étapes de test ici
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
            script {
                sh 'curl -X POST "http://host.docker.internal:8081/api/jenkins-logs/webhook?jobName=stocksens&buildNumber=${BUILD_NUMBER}&buildStatus=SUCCESS&token=test"'
            }
        }

        failure {
            echo '❌ Build failed!'
            script {
                sh 'curl -X POST "http://host.docker.internal:8081/api/jenkins-logs/webhook?jobName=stocksens&buildNumber=${BUILD_NUMBER}&buildStatus=FAILURE&token=test"'
            }
        }
    }
}

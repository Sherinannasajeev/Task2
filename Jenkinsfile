pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sherinannasajeev/Task2.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Redirect output to log file using Windows syntax
                bat 'npm test > test-output.log 2>&1'
            }
            post {
                success {
                    emailext subject: "TEST PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Test stage succeeded.\nCheck build details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'test-output.log'
                }
                failure {
                    emailext subject: "TEST FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Test stage failed.\nCheck build details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'test-output.log'
                }
            }
        }

        stage('Security Scan') {
            steps {
                bat 'npm run security-scan > security-output.log 2>&1'
            }
            post {
                success {
                    emailext subject: "SECURITY SCAN PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Security scan succeeded.\nCheck build details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'security-output.log'
                }
                failure {
                    emailext subject: "SECURITY SCAN FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Security scan failed.\nCheck build details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'security-output.log'
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo Deploying application...'
                // Replace this with your real deployment commands for Windows
            }
            post {
                success {
                    emailext subject: "DEPLOYMENT SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Deployment completed successfully.\nCheck build at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com"
                }
                failure {
                    emailext subject: "DEPLOYMENT FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Deployment failed.\nCheck build at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com"
                }
            }
        }

    }
}

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
                bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
            }
        }

        stage('Test') {
            steps {
                // Catch errors so the stage failing won't fail the pipeline
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat '"C:\\Program Files\\nodejs\\npm.cmd" test > test-output.log 2>&1'
                }
            }
            post {
                always {
                    emailext subject: "TEST RESULT: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Check test details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'test-output.log'
                }
            }
        }

        stage('Security Scan') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat '"C:\\Program Files\\nodejs\\npm.cmd" run security-scan > security-output.log 2>&1'
                }
            }
            post {
                always {
                    emailext subject: "SECURITY SCAN RESULT: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Check security scan details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com",
                             attachLog: true,
                             attachmentsPattern: 'security-output.log'
                }
            }
        }

        stage('Deploy') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat 'echo Deploying application...'
                }
            }
            post {
                always {
                    emailext subject: "DEPLOYMENT RESULT: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                             body: "Check deployment details at ${env.BUILD_URL}",
                             to: "sherinsajeevpaul@gmail.com"
                }
            }
        }

    }
}

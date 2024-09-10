pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium'
            }
            post {
                success {
                    emailext(
                        to: 'emailjenkins55@gmail.com',
                        subject: "SUCCESS: Unit and Integration Tests - ${currentBuild.fullDisplayName}",
                        body: "Unit and Integration Tests Completed Successfully: ${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: 'logs/**/*.log', // Adjust the pattern to where your logs are stored
                        mimeType: 'text/plain'
                    )
                }
                failure {
                    emailext(
                        to: 'emailjenkins55@gmail.com',
                        subject: "FAILURE: Unit and Integration Tests - ${currentBuild.fullDisplayName}",
                        body: "Unit and Integration Tests Failed: ${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: 'logs/**/*.log', // Adjust the pattern to where your logs are stored
                        mimeType: 'text/plain'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
            }
            post {
                success {
                    emailext(
                        to: 'emailjenkins55@gmail.com',
                        subject: "SUCCESS: Security Scan - ${currentBuild.fullDisplayName}",
                        body: "Security Scan Completed Successfully: ${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: 'logs/**/*.log', // Adjust the pattern to where your logs are stored
                        mimeType: 'text/plain'
                    )
                }
                failure {
                    emailext(
                        to: 'emailjenkins55@gmail.com',
                        subject: "FAILURE: Security Scan - ${currentBuild.fullDisplayName}",
                        body: "Security Scan Failed: ${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: 'logs/**/*.log', // Adjust the pattern to where your logs are stored
                        mimeType: 'text/plain'
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 production server'
            }
        }
    }
    post {
        always {
            echo 'This is a general notification that the job has completed. Check individual stages for specific results.'
        }
    }
}

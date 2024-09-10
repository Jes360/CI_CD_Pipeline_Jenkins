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
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "SUCCESS: Unit and Integration Tests - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "Unit and Integration Tests Completed Successfully: ${env.JOB_NAME} #${env.BUILD_NUMBER}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: '**/target/surefire-reports/*.xml', // Assuming test reports are XML files in the target directory
                        mimeType: 'application/xml'
                    )
                }
                failure {
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "FAILURE: Unit and Integration Tests - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "Unit and Integration Tests Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: '**/target/surefire-reports/*.xml', // Assuming test reports are XML files in the target directory
                        mimeType: 'application/xml'
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
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "SUCCESS: Security Scan - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "Security Scan Completed Successfully: ${env.JOB_NAME} #${env.BUILD_NUMBER}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: '**/security-reports/*.json', // Assuming security reports are JSON files
                        mimeType: 'application/json'
                    )
                }
                failure {
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "FAILURE: Security Scan - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "Security Scan Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}\nCheck console output at ${env.BUILD_URL}.",
                        attachmentsPattern: '**/security-reports/*.json', // Assuming security reports are JSON files
                        mimeType: 'application/json'
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

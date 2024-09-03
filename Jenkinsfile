pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven'
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium'
                // Example: sh 'run-tests.sh'
            }
            post {
                always {
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "Completed: Unit and Integration Tests - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """<p>Tests completed with status: ${currentBuild.currentResult}</p>
                                 <p>View detailed test results at: <a href="${env.BUILD_URL}console">Build Console</a></p>""",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // Example: sh 'sonarqube-analysis.sh'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                // Example: sh 'zap-security-scan.sh'
            }
            post {
                always {
                    emailext (
                        to: 'emailjenkins55@gmail.com',
                        subject: "Completed: Security Scan - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """<p>Security scan completed with status: ${currentBuild.currentResult}</p>
                                 <p>View security scan details at: <a href="${env.BUILD_URL}console">Build Console</a></p>""",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server'
                // Example: sh 'deploy-staging.sh'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                // Example: sh 'integration-tests-staging.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 production server'
                // Example: sh 'deploy-production.sh'
            }
        }
    }
}

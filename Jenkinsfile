pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'emailjenkins55@gmail.com'
        LOG_FILE = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Github\\final-pipeline-log.txt"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    BUILD_LOGS = "Building the code...,Build tool: Maven\n "
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    TEST_LOGS = " Running unit and integration tests...,Test tools: JUnit, Selenium "
                }
            }
            post {
                always {
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Jenkins Notification - Unit and Integration Tests Completed for Build #${env.BUILD_NUMBER}",
                        body: "Unit and Integration Tests have completed for Build #${env.BUILD_NUMBER}.Please check Jenkins for more details.",
                        mimeType: 'text/plain'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    CODE_ANALYSIS_LOGS = " Analyzing code quality...,Code analysis tool: SonarQube "
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    SECURITY_SCAN_LOGS = " Performing security scan...,Security scan tool: OWASP Dependency Check "
                }
            }
            post {
                always {
                    emailext(
                        to: "${env.RECIPIENT_EMAIL}",
                        subject: "Jenkins Notification - Security Scan Completed for Build #${env.BUILD_NUMBER}",
                        body: "Security Scan has completed for Build #${env.BUILD_NUMBER}.Please check Jenkins for detailed results.",
                        mimeType: 'text/plain'
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    DEPLOY_STAGING_LOGS = " Deploying to staging environment...,Deploying to ${env.STAGING_SERVER} "
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    INTEGRATION_STAGING_LOGS = " Running integration tests on staging... "
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    DEPLOY_PROD_LOGS = " Deploying to production environment...,Deploying to ${env.PRODUCTION_SERVER} "
                }
            }
        }
    }
    post {
        always {
            script {
                // Combine all log strings into one final log message and write to the log file
                FINAL_LOGS = BUILD_LOGS  + TEST_LOGS + CODE_ANALYSIS_LOGS + SECURITY_SCAN_LOGS +
                             DEPLOY_STAGING_LOGS + INTEGRATION_STAGING_LOGS + DEPLOY_PROD_LOGS
                bat "echo ${FINAL_LOGS.replace('\n', '^n')} > ${LOG_FILE}"
            }
            emailext(
                attachLog: true,
                attachmentsPattern: "final-pipeline-log.txt",
                subject: "Jenkins Build Log - Build #${env.BUILD_NUMBER}",
                body: "Build #${env.BUILD_NUMBER} has completed. Please find the attached log file for details.",
                to: "${env.RECIPIENT_EMAIL}",
                mimeType: 'text/plain'
            )
        }
    }
}

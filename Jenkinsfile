pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'emailjenkins55@gmail.com'
        // Define a simple log file name
        LOG_FILE = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Github\\final-pipeline-log.txt"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Collect logs in environment variables or use script to append to a string
                    BUILD_LOGS = "Building the code...\\nBuild tool: Maven\\n"
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    TEST_LOGS = "Running unit and integration tests...\\nTest tools: JUnit, Selenium\\n"
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    CODE_ANALYSIS_LOGS = "Analyzing code quality...\\nCode analysis tool: SonarQube\\n"
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    SECURITY_SCAN_LOGS = "Performing security scan...\\nSecurity scan tool: OWASP Dependency Check\\n"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    DEPLOY_STAGING_LOGS = "Deploying to staging environment...\\nDeploying to ${env.STAGING_SERVER}\\n"
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    INTEGRATION_STAGING_LOGS = "Running integration tests on staging...\\n"
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    DEPLOY_PROD_LOGS = "Deploying to production environment...\\nDeploying to ${env.PRODUCTION_SERVER}\\n"
                }
            }
        }
    }
    post {
        always {
            script {
                // Combine all log strings into one final log message
                FINAL_LOGS = BUILD_LOGS + TEST_LOGS + CODE_ANALYSIS_LOGS + SECURITY_SCAN_LOGS +
                             DEPLOY_STAGING_LOGS + INTEGRATION_STAGING_LOGS + DEPLOY_PROD_LOGS
                // Write the final logs to the log file
                bat "echo ${FINAL_LOGS} > ${LOG_FILE}"
            }
            emailext (
                to: "emailjenkins55@gmail.com",
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: "The pipeline has completed with status: ${currentBuild.currentResult}.\\nPlease find the attached logs for more details.",
                attachmentsPattern: "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Github\\final-pipeline-log.txt",
                mimeType: 'text/plain'
            )
            // Optionally delete the log file if no longer needed
            // bat "del ${LOG_FILE}"
        }
    }
}

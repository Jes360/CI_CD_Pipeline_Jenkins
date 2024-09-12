pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'emailjenkins55@gmail.com'
        // Define log file path in the Jenkins workspace
        LOG_FILE = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Github\\final-pipeline-log.txt"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    BUILD_LOGS = "Building the code...\\nBuild tool: Maven\\n"
                    // Append to BUILD_LOGS or write directly to a temp log if needed
                }
                echo 'Building the code...'
                echo 'Build tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    TEST_LOGS = "Running unit and integration tests...\\nTest tools: JUnit, Selenium\\n"
                }
                echo 'Running unit and integration tests...'
                echo 'Test tools: JUnit, Selenium'
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    CODE_ANALYSIS_LOGS = "Analyzing code quality...\\nCode analysis tool: SonarQube\\n"
                }
                echo 'Analyzing code quality...'
                echo 'Code analysis tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    SECURITY_SCAN_LOGS = "Performing security scan...\\nSecurity scan tool: OWASP Dependency Check\\n"
                }
                echo 'Performing security scan...'
                echo 'Security scan tool: OWASP Dependency Check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    DEPLOY_STAGING_LOGS = "Deploying to staging environment...\\nDeploying to ${env.STAGING_SERVER}\\n"
                }
                echo 'Deploying to staging environment...'
                echo "Deploying to ${env.STAGING_SERVER}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    INTEGRATION_STAGING_LOGS = "Running integration tests on staging...\\n"
                }
                echo 'Running integration tests on staging...'
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    DEPLOY_PROD_LOGS = "Deploying to production environment...\\nDeploying to ${env.PRODUCTION_SERVER}\\n"
                }
                echo 'Deploying to production environment...'
                echo "Deploying to ${env.PRODUCTION_SERVER}"
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
            // Send email with the log file attached
            emailext (
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: "The pipeline has completed with status: ${currentBuild.currentResult}.\nPlease find the attached logs for more details.",
                attachmentsPattern: "${LOG_FILE}",
                mimeType: 'text/plain'
            )
            // Clean up the log file after sending the email
            bat "del ${LOG_FILE}"
        }
    }
}

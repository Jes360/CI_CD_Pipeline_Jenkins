pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'emailjenkins55@gmail.com'
        LOG_FILE = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Github\\final-pipeline-log.txt"
    }
    stages {
        // Define all your stages here as previously discussed
        // Each stage updates its respective logs variable
    }
    post {
        always {
            script {
                // Combine all logs into one final log string
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
                attachmentsPattern: "${LOG_FILE}", // Make sure this pattern exactly matches the log file path
                mimeType: 'text/plain'
            )
            // Optionally, delete the log file after sending the email
            // bat "del ${LOG_FILE}"
        }
    }
}

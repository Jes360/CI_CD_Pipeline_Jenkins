pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'emailjenkins55@gmail.com'
        // Set the log file location within the workspace for easier Ant pattern matching
        LOG_FILE = "pipeline-log-${env.BUILD_ID}.txt"
        LOG_DIR = "logs"  // Using a directory within the workspace to store logs
    }
    stages {
        stage('Setup') {
            steps {
                // Ensure the log directory exists
                bat "if not exist ${WORKSPACE}\\${LOG_DIR} mkdir ${WORKSPACE}\\${LOG_DIR}"
            }
        }
        stage('Build') {
            steps {
                // Using a log directory for easier pattern matching
                bat "echo Building the code... > ${WORKSPACE}\\${LOG_DIR}\\${LOG_FILE}"
                bat "echo Build tool: Maven >> ${WORKSPACE}\\${LOG_DIR}\\${LOG_FILE}"
            }
        }
        // Additional stages would follow the same pattern for logging
    }
    post {
        always {
            echo 'Pipeline completed with status: ' + currentBuild.currentResult
            emailext (
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: """The pipeline has completed with status: ${currentBuild.currentResult}.
                         Please find the attached logs for more details.""",
                // Correct Ant glob pattern to find logs in the designated log directory
                attachmentsPattern: "**/${LOG_DIR}/${LOG_FILE}",
                mimeType: 'text/plain'
            )
            // Cleanup the log file after sending the email
            bat "del ${WORKSPACE}\\${LOG_DIR}\\${LOG_FILE}"
        }
    }
}

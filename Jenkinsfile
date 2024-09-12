pipeline {
    agent any
    environment {
        STAGING_SERVER = 'staging-server.example.com'
        PRODUCTION_SERVER = 'production-server.example.com'
        RECIPIENT_EMAIL = 'raaidrushdy@gmail.com'
        // Define log file path for Windows
        LOG_FILE = "pipeline-log-${env.BUILD_ID}.txt"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Build tool: Maven'
                // Windows batch commands to write to log file
                bat "echo Building the code... > ${LOG_FILE}"
                bat "echo Build tool: Maven >> ${LOG_FILE}"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Test tools: JUnit, Selenium'
                // Append to log file using Windows batch commands
                bat "echo Running unit and integration tests... >> ${LOG_FILE}"
                bat "echo Test tools: JUnit, Selenium >> ${LOG_FILE}"
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                echo 'Code analysis tool: SonarQube'
                // Log this stage using batch commands
                bat "echo Analyzing code quality... >> ${LOG_FILE}"
                bat "echo Code analysis tool: SonarQube >> ${LOG_FILE}"
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                echo 'Security scan tool: OWASP Dependency Check'
                // Security scan details logged using batch commands
                bat "echo Performing security scan... >> ${LOG_FILE}"
                bat "echo Security scan tool: OWASP Dependency Check >> ${LOG_FILE}"
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo "Deploying to ${env.STAGING_SERVER}"
                // Log deployment actions using batch commands
                bat "echo Deploying to staging environment... >> ${LOG_FILE}"
                bat "echo Deploying to ${env.STAGING_SERVER} >> ${LOG_FILE}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Append to log using batch commands
                bat "echo Running integration tests on staging... >> ${LOG_FILE}"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                echo "Deploying to ${env.PRODUCTION_SERVER}"
                // Log deployment details using batch commands
                bat "echo Deploying to production environment... >> ${LOG_FILE}"
                bat "echo Deploying to ${env.PRODUCTION_SERVER} >> ${LOG_FILE}"
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed with status: ' + currentBuild.currentResult
            // Attach the log file to the email using correct Ant glob pattern
            emailext (
                to: "${env.RECIPIENT_EMAIL}",
                subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: """The pipeline has completed with status: ${currentBuild.currentResult}.
                         Please find the attached logs for more details.""",
                attachmentsPattern: "**/${LOG_FILE}",
                mimeType: 'text/plain'
            )
            // Clean up the log file after sending the email using Windows batch command
            bat "del ${LOG_FILE}"
        }
    }
}

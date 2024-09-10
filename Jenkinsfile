pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven'
                sh 'mvn clean package' // This actually builds the application and generates logs and artifacts.
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium'
                sh 'mvn test' // Executes tests and generates test reports.
            }
        }
        // Additional stages as needed...
    }
    post {
        always {
            // Gather detailed information
            def buildStatus = currentBuild.currentResult
            def buildUrl = "${env.BUILD_URL}"
            def jobName = "${env.JOB_NAME}"
            def buildNumber = "${env.BUILD_NUMBER}"

            // Construct the email body
            def emailBody = """
                <h1>Build Report - ${jobName} #${buildNumber}</h1>
                <p>Status: <strong>${buildStatus}</strong></p>
                <p>Build details are available at: <a href='${buildUrl}'>${buildUrl}</a></p>
                <p>Please find attached the logs and test reports for more details.</p>
            """

            // Send email with attachments
            emailext(
                to: 'emailjenkins55@gmail.com',
                subject: "Build Notification: ${jobName} #${buildNumber}",
                body: emailBody,
                attachmentsPattern: '**/target/*.log,**/target/surefire-reports/*.xml', // Attach build logs and test reports
                mimeType: 'text/html'
            )
        }
    }
}

pipeline {
    agent any

    stages {
        // Define your stages as before
    }
    post {
        always {
            // Checks if Email Extension plugin is properly referenced
            emailext (
                recipients: 'emailjenkins55@gmail.com',
                subject: "Jenkins Build Notification: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>The build was ${currentBuild.currentResult}.</p>
                         <p>See more details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                attachLog: true
            )
        }
    }
}

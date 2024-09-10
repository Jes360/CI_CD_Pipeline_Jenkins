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
   post {
    always {
        emailext (
            to: 'emailjenkins55@gmail.com',
            subject: "Build Results for ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Please see the attached logs for details of the build.",
            attachmentsPattern: '**/logs/*.log', // Adjust the pattern according to where logs are stored
            mimeType: 'text/plain'
        )
    }
}

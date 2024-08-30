pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven'
                // Maven could be invoked here if implementing: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium'
                // Commands to run JUnit and Selenium tests would be placed here
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // SonarQube analysis command could be here
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                // OWASP ZAP scanning commands could go here
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server'
                // Deployment scripts to AWS EC2
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                // Integration testing commands in the staging environment
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 production server'
                // Deployment scripts to AWS EC2
            }
        }
    }
    post {
        always {
            mail bcc: '', body: "Stage Completed: ${currentBuild.currentResult}\nCheck console output at ${env.BUILD_URL} to view test results.", cc: '', from: '', replyTo: '', subject: "Pipeline Notification: ${currentBuild.fullDisplayName}", to: "emailjenkins55@gmail.com"
        }
    }
}

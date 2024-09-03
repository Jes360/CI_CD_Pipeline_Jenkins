pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven'
                // Example command: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium'
                // Example command: sh 'run-tests.sh'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // Example command: sh 'sonarqube-analysis.sh'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                // Example command: sh 'zap-security-scan.sh'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging server'
                // Example command: sh 'deploy-staging.sh'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                // Example command: sh 'integration-tests-staging.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 production server'
                // Example command: sh 'deploy-production.sh'
            }
        }
    }
    post {
        always {
            emailext (
                to: 'emailjenkins55@gmail.com',
                subject: "Jenkins Build Notification: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>The build was ${currentBuild.currentResult}.</p>
                         <p>See more details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                attachLog: true
            )
        }
    }
}

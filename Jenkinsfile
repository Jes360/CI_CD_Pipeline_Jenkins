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
        post {
        always {
        emailext (
            recipients: 'your-email@example.com',
            subject: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            body: "The build has finished with status: ${currentBuild.currentResult}\nCheck details at: ${env.BUILD_URL}",
            attachLog: false
        )
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

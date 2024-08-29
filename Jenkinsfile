pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage: Building the application using Maven.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Test stage: Running unit tests with JUnit and integration tests with Selenium.'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Code Analysis stage: Analyzing code with SonarQube to ensure it meets industry standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Security Scan stage: Performing security scan using OWASP ZAP to identify any vulnerabilities.'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deployment stage: Deploying the application to a staging server using AWS EC2.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Integration Testing stage: Running integration tests on the staging environment to ensure functionality.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Production Deployment stage: Deploying the application to a production server, also using AWS EC2.'
            }
        }
    }
    post {
        always {
            echo 'This is a post-build step to notify stakeholders of the build status.'
        }
    }
}

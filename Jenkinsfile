pipeline {
agent any
stages {
stage('Build') {
steps {
echo 'Building the application using Maven'
}
}
stage('Unit and Integration Tests') {
steps {
echo 'Running unit and integration tests using JUnit and Selenium'
}
post {
success {
mail bcc: '',
body: "Unit and Integration Tests Completed Successfully:
${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
subject: "SUCCESS: Unit and Integration Tests -
${currentBuild.fullDisplayName}",
to: "emailjenkins55@gmail.com"
}
failure {
mail bcc: '',
body: "Unit and Integration Tests Failed:
${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
subject: "FAILURE: Unit and Integration Tests -
${currentBuild.fullDisplayName}",
to: "emailjenkins55@gmail.com"
}
}
}
stage('Code Analysis') {
steps {
echo 'Analyzing code with SonarQube'
}
}
stage('Security Scan') {
steps {
echo 'Performing security scan using OWASP ZAP'
}
post {
success {
mail bcc: '',
body: "Security Scan Completed Successfully:
${currentBuild.fullDisplayName}\nCheck console output at ${env.BUILD_URL}.",
subject: "SUCCESS: Security Scan - ${currentBuild.fullDisplayName}",
to: "emailjenkins55@gmail.com"
}
failure {
mail bcc: '',
body: "Security Scan Failed: ${currentBuild.fullDisplayName}\nCheck
console output at ${env.BUILD_URL}.",
subject: "FAILURE: Security Scan - ${currentBuild.fullDisplayName}",
to: "emailjenkins55@gmail.com"
}
}
}
stage('Deploy to Staging') {
steps {
echo 'Deploying to AWS EC2 staging server'
}
}
stage('Integration Tests on Staging') {
steps {
echo 'Running integration tests on staging environment'
}
}
stage('Deploy to Production') {
steps {
echo 'Deploying to AWS EC2 production server'
}
}
}
post {
always {
echo 'This is a general notification that the job has completed. Check individual
stages for specific results.'
}
}
}

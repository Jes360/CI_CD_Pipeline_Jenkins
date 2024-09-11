pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Running build and capturing output into a log file
                    sh 'mvn clean package > ${WORKSPACE}/build.log 2>&1'
                }
            }
        }
    }
    post {
        always {
            // Assuming build.log is generated, email it
            emailext (
                to: 'email@example.com',
                subject: "Build Results for ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Attached are the build logs.",
                attachmentsPattern: 'build.log',
                mimeType: 'text/plain'
            )
        }
    }
}

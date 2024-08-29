pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'C:\Users\jesti\OneDrive - Deakin University\Desktop\SIT223\4.1Gp\Deakin-Unit-Page'
        TESTING_ENVIRONMENT = 'test-environment'
        PRODUCTION_ENVIRONMENT = 'Jes'
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy the application to the testing environment: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo "Pausing for manual approval"
                sleep 10
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}

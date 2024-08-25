pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '.'
        TESTING_ENVIRONMENT = 'testjenkin'
        PRODUCTION_ENVIRONMENT = 'testproduct'
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
                echo 'Running unit tests'
                echo 'Running integration tests'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Checking the quality of the code'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to the testing environment: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo 'Waiting for manual approval...'
                sleep 10
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}

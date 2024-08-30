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
                // Example: sh 'mvn clean package' or bat 'gradlew build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests'
                echo 'Running integration tests'
                // Example: sh 'mvn test' or bat 'gradlew test'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Checking the quality of the code'
                // Example: sh 'sonar-scanner' or any code quality tool command
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to the testing environment: ${env.TESTING_ENVIRONMENT}"
                // Example: sh './deploy-to-test-env.sh' or bat 'deploy-to-test-env.bat'
            }
        }
        stage('Approval') {
            steps {
                input message: 'Do you want to proceed with deployment to production?', ok: 'Deploy to Production'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
                // Example: sh './deploy-to-production.sh' or bat 'deploy-to-production.bat'
            }
        }
    }

    post {
        success {
            mail to: 'disuru.office@gmail.com',
                 subject: "Pipeline Completed Successfully",
                 body: "All stages completed successfully. Logs are attached."
        }
        failure {
            mail to: 'disuru.office@gmail.com',
                 subject: "Pipeline Failed",
                 body: "The pipeline failed. Please check the logs."
        }
    }
}

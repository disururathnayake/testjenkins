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
                echo "Using Maven to build the code"
                // Example: sh 'mvn clean package'
            }
            post {
                success {
                    echo "Build successful."
                }
                failure {
                    echo "Build failed."
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Using JUnit for unit testing'
                echo 'Using Selenium for integration testing'
                // Example: sh 'mvn test'
            }
            post {
                success {
                    emailext to: 'disuru.office@gmail.com',
                             subject: "Testing Stage Completed Successfully",
                             body: "Unit and integration tests passed.",
                             attachLog: true
                }
                failure {
                    emailext to: 'disuru.office@gmail.com',
                             subject: "Testing Stage Failed",
                             body: "Some tests failed. Check the logs.",
                             attachLog: true
                }
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Using SonarQube for code quality analysis'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Using OWASP ZAP for security scanning'
                // Example: sh './security-scan.sh'
            }
            post {
                success {
                    emailext to: 'disuru.office@gmail.com',
                             subject: "Security Scan Completed Successfully",
                             body: "No vulnerabilities found.",
                             attachLog: true
                }
                failure {
                    emailext to: 'disuru.office@gmail.com',
                             subject: "Security Scan Failed",
                             body: "Vulnerabilities detected. Check the logs.",
                             attachLog: true
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment: ${env.TESTING_ENVIRONMENT}"
                // Example: sh './deploy-to-staging.sh'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging'
                // Example: sh 'mvn verify'
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
                // Example: sh './deploy-to-production.sh'
            }
        }
    }

    post {
        always {
            echo 'This will always run at the end of the pipeline.'
        }
        success {
            emailext to: 'disuru.office@gmail.com',
                     subject: "Pipeline Completed Successfully",
                     body: "All stages completed successfully. Logs are attached.",
                     attachLog: true
        }
        failure {
            emailext to: 'disuru.office@gmail.com',
                     subject: "Pipeline Failed",
                     body: "The pipeline failed. Please check the logs.",
                     attachLog: true
        }
    }
}

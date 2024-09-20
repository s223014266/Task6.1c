pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "${env.WORKSPACE}"
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'Anushka'
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from ${env.DIRECTORY_PATH}"
                echo "Compiling the code and generating necessary artifacts"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit"
                echo "Running integration tests using TestNG"
            }

            post{
                success{
                    emailext(
                        to: "anushka7k@gmail.com",
                        subject: "Unit and Integration Tests Passed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                        body: "Unit and integration tests have passed.",
                        attachLog: true
                    )
                }

                failure {
                    emailext (
                        to: "anushka7k@gmail.com",
                        subject: "Unit and Integration Tests Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                        body: "Unit and integration tests have failed. Check the logs for more details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Analyzing code quality using SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing a security scan using OWASP ZAP"
            }

            post{
                success {
                    emailext (
                        to: "anushka7k@gmail.com",
                        subject: "Security Scan Completed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                        body: "Security scan completed successfully.",
                        attachLog: true
                    )
                }

                failure {
                    emailext (
                        to: "anushka7k@gmail.com",
                        subject: "Security Scan Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                        body: "Security scan failed. Check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to ${env.TESTING_ENVIRONMENT} environment"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to the ${env.PRODUCTION_ENVIRONMENT} environment"
            }
        }
    }
}

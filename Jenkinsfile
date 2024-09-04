pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Fetching the source code'
                echo 'Compiling the code and generating necessary artifacts'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests using JUnit'
                echo 'Running integration tests using TestNG'
            }
        }

        stage('Code Analysis') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('UNSTABLE') }
            }
            steps {
                echo 'Running static code analysis'
            }
        }

        stage('Security Scan') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('UNSTABLE') }
            }
            steps {
                echo 'Running security scans'
            }
        }

        stage('Deploy to Staging') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('UNSTABLE') }
            }
            steps {
                echo 'Deploying to staging environment'
            }
        }

        stage('Integration Tests on Staging') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('UNSTABLE') }
            }
            steps {
                echo 'Running integration tests on staging environment'
            }
        }

        stage('Deploy to Production') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('UNSTABLE') }
            }
            steps {
                echo 'Deploying to production environment'
            }
        }
    }

    post {
        success {
            mail to: 'anushka7k@gmail.com',
                 subject: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${currentBuild.currentResult})",
                 body: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed successfully."
        }
        failure {
            mail to: 'anushka7k@gmail.com',
                 subject: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${currentBuild.currentResult})",
                 body: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' failed. Please check the Jenkins console output."
        }
    }
}

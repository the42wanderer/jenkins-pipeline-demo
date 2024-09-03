pipeline {
    agent any

    environment {
        // Set the email notification recipients
        EMAIL_RECIPIENTS = 'danidukarunarathne@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Uncomment and adjust as needed
                // sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Uncomment and adjust as needed
                // sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                // Uncomment and adjust as needed
                // sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities using OWASP Dependency-Check...'
                // Uncomment and adjust as needed
                // sh 'dependency-check.sh --project your-project-name --out .'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging server...'
                // Uncomment and adjust as needed
                // sh 'aws deploy ...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment...'
                // Uncomment and adjust as needed
                // sh 'mvn verify'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production server...'
                // Uncomment and adjust as needed
                // sh 'aws deploy ...'
            }
        }
    }

    post {
        always {
            // Archive all log files in the workspace
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
        success {
            script {
                echo 'Sending success email...'
                emailext (
                    subject: "SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                    body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] succeeded.",
                    to: "${env.EMAIL_RECIPIENTS}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
        failure {
            script {
                echo 'Sending failure email...'
                emailext (
                    subject: "FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                    body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed.",
                    to: "${env.EMAIL_RECIPIENTS}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
    }
}

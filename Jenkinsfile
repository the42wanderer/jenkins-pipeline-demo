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
                // Example command to build the project with Maven
                // sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example command to run tests (JUnit, TestNG, etc.)
                // sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                // Example command for code analysis (using SonarQube)
                // sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities using OWASP Dependency-Check...'
                // Example command to perform a security scan
                // sh 'dependency-check.sh --project your-project-name --out .'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging server...'
                // Example command to deploy to an AWS EC2 instance
                // sh 'aws deploy ...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment...'
                // Example command to run integration tests
                // sh 'mvn verify'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production server...'
                // Example command to deploy to a production AWS EC2 instance
                // sh 'aws deploy ...'
            }
        }
    }
    post {
    always {
        archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
    }
    success {
        emailext (
            subject: "SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
            body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] succeeded.",
            to: "${env.EMAIL_RECIPIENTS}",
            attachmentsPattern: '**/*.log'
        )
    }
    failure {
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

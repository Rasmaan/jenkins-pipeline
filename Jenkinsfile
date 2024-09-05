pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application...'
                // sh 'mvn clean package' // Replace this with the actual build command if needed
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // sh 'mvn test'
                // sh 'mvn integration-test'
                script {
                    // Capture logs and save to a file
                    echo 'Capturing logs for Unit and Integration Tests...'
                    sh 'echo "Unit and Integration Test logs" > unit-tests-log.txt' // Replace with actual log command if needed
                }
            }
            post {
                success {
                    // Archive the log file
                    archiveArtifacts artifacts: 'unit-tests-log.txt', allowEmptyArchive: true
                    script {
                        // Send success email with log attachment
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Unit and Integration Tests Successful: ${currentBuild.fullDisplayName}",
                             body: "The Unit and Integration Tests stage has completed successfully.",
                             attachmentsPattern: 'unit-tests-log.txt'
                    }
                }
                failure {
                    // Archive the log file
                    archiveArtifacts artifacts: 'unit-tests-log.txt', allowEmptyArchive: true
                    script {
                        // Send failure email with log attachment
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Unit and Integration Tests Failed: ${currentBuild.fullDisplayName}",
                             body: "The Unit and Integration Tests stage has failed. Please check the attached logs.",
                             attachmentsPattern: 'unit-tests-log.txt'
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // sh 'mvn sonar:sonar' // Replace with the actual command if needed
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // sh 'mvn dependency-check:check'
                script {
                    // Capture logs and save to a file
                    echo 'Capturing logs for Security Scan...'
                    sh 'echo "Security Scan logs" > security-scan-log.txt' // Replace with actual log command if needed
                }
            }
            post {
                success {
                    // Archive the log file
                    archiveArtifacts artifacts: 'security-scan-log.txt', allowEmptyArchive: true
                    script {
                        // Send success email with log attachment
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has completed successfully.",
                             attachmentsPattern: 'security-scan-log.txt'
                    }
                }
                failure {
                    // Archive the log file
                    archiveArtifacts artifacts: 'security-scan-log.txt', allowEmptyArchive: true
                    script {
                        // Send failure email with log attachment
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has failed. Please check the attached logs.",
                             attachmentsPattern: 'security-scan-log.txt'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // sh 'cp target/app.jar /staging-server/deploy/app.jar' // Replace with actual command if needed
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // sh 'mvn test -Pstaging' // Replace with the actual command if needed
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // sh 'cp target/app.jar /production-server/deploy/app.jar' // Replace with actual command if needed
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
        success {
            mail to: 'rasmaananwar123@gmail.com',
                 subject: "Pipeline Successful: ${currentBuild.fullDisplayName}",
                 body: "The Jenkins pipeline has completed successfully."
        }
        failure {
            mail to: 'rasmaananwar123@gmail.com',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "The Jenkins pipeline has failed. Please check the logs."
        }
    }
}

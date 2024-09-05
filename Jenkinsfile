pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use sh for Unix-based systems
                // sh 'mvn clean package'
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
                // List the contents of the workspace to verify the log file is present
                sh 'pwd' // Print the current working directory
                sh 'ls -l' // List all files in the current directory
            }
            post {
                success {
                    archiveArtifacts artifacts: 'unit-tests-log.txt', allowEmptyArchive: true
                    script {
                        // Send success email with log attachment using emailext
                        emailext attachmentsPattern: 'unit-tests-log.txt',
                                 to: 'rasmaananwar123@gmail.com',
                                 subject: "Unit and Integration Tests Successful: ${currentBuild.fullDisplayName}",
                                 body: "The Unit and Integration Tests stage has completed successfully."
                    }
                }
                failure {
                    archiveArtifacts artifacts: 'unit-tests-log.txt', allowEmptyArchive: true
                    script {
                        // Send failure email with log attachment using emailext
                        emailext attachmentsPattern: 'unit-tests-log.txt',
                                 to: 'rasmaananwar123@gmail.com',
                                 subject: "Unit and Integration Tests Failed: ${currentBuild.fullDisplayName}",
                                 body: "The Unit and Integration Tests stage has failed. Please check the attached logs."
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
                // List the contents of the workspace to verify the log file is present
                sh 'pwd' // Print the current working directory
                sh 'ls -l' // List all files in the current directory
            }
            post {
                success {
                    archiveArtifacts artifacts: 'security-scan-log.txt', allowEmptyArchive: true
                    script {
                        // Send success email with log attachment using emailext
                        emailext attachmentsPattern: 'security-scan-log.txt',
                                 to: 'rasmaananwar123@gmail.com',
                                 subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                                 body: "The Security Scan stage has completed successfully."
                    }
                }
                failure {
                    archiveArtifacts artifacts: 'security-scan-log.txt', allowEmptyArchive: true
                    script {
                        // Send failure email with log attachment using emailext
                        emailext attachmentsPattern: 'security-scan-log.txt',
                                 to: 'rasmaananwar123@gmail.com',
                                 subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                                 body: "The Security Scan stage has failed. Please check the attached logs."
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
            emailext to: 'rasmaananwar123@gmail.com',
                     subject: "Pipeline Successful: ${currentBuild.fullDisplayName}",
                     body: "The Jenkins pipeline has completed successfully."
        }
        failure {
            emailext to: 'rasmaananwar123@gmail.com',
                     subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                     body: "The Jenkins pipeline has failed. Please check the logs."
        }
    }
}

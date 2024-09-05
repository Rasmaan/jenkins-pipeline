pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example: Capturing the build logs
                sh 'mvn clean package > build-log.txt 2>&1' // Replace with your actual build command
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example: Capturing the output of test commands
                sh 'mvn test > unit-tests-log.txt 2>&1' // Replace with actual test command
                sh 'mvn integration-test >> unit-tests-log.txt 2>&1' // Append integration test logs
                // List the contents of the workspace to verify the log file is present
                sh 'pwd' // Print the current working directory
                sh 'ls -l' // List all files in the current directory
            }
            post {
                success {
                    script {
                        // Read the log content
                        def logContent = readFile('unit-tests-log.txt')
                        // Send success email with log content in the body
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Unit and Integration Tests Successful: ${currentBuild.fullDisplayName}",
                             body: "The Unit and Integration Tests stage has completed successfully.\n\nLog Details:\n${logContent}"
                    }
                }
                failure {
                    script {
                        // Read the log content
                        def logContent = readFile('unit-tests-log.txt')
                        // Send failure email with log content in the body
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Unit and Integration Tests Failed: ${currentBuild.fullDisplayName}",
                             body: "The Unit and Integration Tests stage has failed. Please check the details below:\n\nLog Details:\n${logContent}"
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Example: Capturing the output of code analysis
                sh 'mvn sonar:sonar > code-analysis-log.txt 2>&1' // Replace with actual command if needed
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Example: Capturing security scan logs
                sh 'mvn dependency-check:check > security-scan-log.txt 2>&1' // Replace with actual log command if needed
                // List the contents of the workspace to verify the log file is present
                sh 'pwd' // Print the current working directory
                sh 'ls -l' // List all files in the current directory
            }
            post {
                success {
                    script {
                        // Read the log content
                        def logContent = readFile('security-scan-log.txt')
                        // Send success email with log content in the body
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has completed successfully.\n\nLog Details:\n${logContent}"
                    }
                }
                failure {
                    script {
                        // Read the log content
                        def logContent = readFile('security-scan-log.txt')
                        // Send failure email with log content in the body
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has failed. Please check the details below:\n\nLog Details:\n${logContent}"
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example: Capturing deploy logs
                sh 'cp target/app.jar /staging-server/deploy/app.jar > deploy-log.txt 2>&1' // Replace with actual command if needed
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example: Capturing integration test logs on staging
                sh 'mvn test -Pstaging > staging-tests-log.txt 2>&1' // Replace with actual command if needed
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example: Capturing deploy to production logs
                sh 'cp target/app.jar /production-server/deploy/app.jar > production-deploy-log.txt 2>&1' // Replace with actual command if needed
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

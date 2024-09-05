pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Using bat instead of sh for Windows
                // bat 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Running tests in Windows environment
                // bat 'mvn test'
                // bat 'mvn integration-test'
            }
        }

        // Send email immediately after the Unit and Integration Tests stage
        stage('Notify After Tests') {
            steps {
                script {
                    def logs = currentBuild.rawBuild.getLog(100).join('\n')
                    writeFile file: 'pipeline-log.txt', text: logs
                    mail to: 'rasmaananwar123@gmail.com',
                         subject: "Unit and Integration Tests Completed: ${currentBuild.fullDisplayName}",
                         body: "The Unit and Integration Tests stage has completed. Please check the attached logs.",
                         attachmentsPattern: 'pipeline-log.txt'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // bat 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // bat 'mvn dependency-check:check'
            }
        }

        // Send email immediately after the Security Scan stage
        stage('Notify After Security Scan') {
            steps {
                script {
                    def logs = currentBuild.rawBuild.getLog(100).join('\n')
                    writeFile file: 'pipeline-log.txt', text: logs
                    mail to: 'rasmaananwar123@gmail.com',
                         subject: "Security Scan Completed: ${currentBuild.fullDisplayName}",
                         body: "The Security Scan stage has completed. Please check the attached logs.",
                         attachmentsPattern: 'pipeline-log.txt'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example deployment command, modify according to your environment
                // bat 'copy target\\app.jar \\\\staging-server\\deploy\\app.jar'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // bat 'mvn test -Pstaging'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example deployment command for production
                // bat 'copy target\\app.jar \\\\production-server\\deploy\\app.jar'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

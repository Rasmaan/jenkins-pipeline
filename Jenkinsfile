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
            post {
                success {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join('\n')
                        writeFile file: 'unit-tests-log.txt', text: logs
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Unit and Integration Tests Successful: ${currentBuild.fullDisplayName}",
                             body: "The Unit and Integration Tests stage has completed successfully.",
                             attachmentsPattern: 'unit-tests-log.txt'
                    }
                }
                failure {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join('\n')
                        writeFile file: 'unit-tests-log.txt', text: logs
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
                // bat 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // bat 'mvn dependency-check:check'
            }
            post {
                success {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join('\n')
                        writeFile file: 'security-scan-log.txt', text: logs
                        mail to: 'rasmaananwar123@gmail.com',
                             subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has completed successfully.",
                             attachmentsPattern: 'security-scan-log.txt'
                    }
                }
                failure {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join('\n')
                        writeFile file: 'security-scan-log.txt', text: logs
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
    }
}

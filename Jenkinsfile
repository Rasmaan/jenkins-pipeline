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

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
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
                // bat 'copy target\\app.jar \\\\production-server\\deploy\\app.jar'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }

        // Sending success email after tests and security scan stages
        stage('Send Success Email') {
            when {
                allOf {
                    successful()
                    stage('Unit and Integration Tests')
                    stage('Security Scan')
                }
            }
            steps {
                script {
                    def logs = currentBuild.rawBuild.getLog(100).join('\n') // Fetch last 100 lines of logs
                    writeFile file: 'pipeline-log.txt', text: logs // Write logs to a file

                    mail to: 'rasmaananwar123@gmail.com',
                         subject: "Pipeline Successful: ${currentBuild.fullDisplayName}",
                         body: "The Jenkins pipeline has completed successfully.",
                         attachmentsPattern: 'pipeline-log.txt' // Attach logs to email
                }
            }
        }

        // Sending failure email after tests and security scan stages
        stage('Send Failure Email') {
            when {
                allOf {
                    failure()
                    stage('Unit and Integration Tests')
                    stage('Security Scan')
                }
            }
            steps {
                script {
                    def logs = currentBuild.rawBuild.getLog(100).join('\n') // Fetch last 100 lines of logs
                    writeFile file: 'pipeline-log.txt', text: logs // Write logs to a file

                    mail to: 'rasmaananwar123@gmail.com',
                         subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                         body: "The Jenkins pipeline has failed. Please check the attached logs.",
                         attachmentsPattern: 'pipeline-log.txt' // Attach logs to email
                }
            }
        }
    }
}

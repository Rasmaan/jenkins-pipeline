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
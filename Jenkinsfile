pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        to: 'rasmaananwar123@gmail.com',
                        subject: "Test Stage Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The Unit and Integration Tests stage completed successfully.\n\nJob Name: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nView details at: ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'rasmaananwar123@gmail.com',
                        subject: "Test Stage Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The Unit and Integration Tests stage failed.\n\nJob Name: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nView details at: ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'dependency-check.sh --project my-app'
            }
            post {
                success {
                    emailext(
                        to: 'rasmaananwar123@gmail.com',
                        subject: "Security Scan Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The Security Scan stage completed successfully.\n\nJob Name: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nView details at: ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'rasmaananwar123@gmail.com',
                        subject: "Security Scan Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The Security Scan stage failed.\n\nJob Name: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nView details at: ${env.BUILD_URL}",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'scp target/my-app.jar ec2-user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'run-staging-tests.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'scp target/my-app.jar ec2-user@production-server:/path/to/deploy'
            }
        }
    }
}

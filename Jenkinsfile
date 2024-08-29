pipeline {
    agent any
    tools {
        gradle 'Gradle' 
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew clean build' 
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh './gradlew test' // Runs tests using Gradle
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
                sh './gradlew check' 
            }
        }
        stage('Security Scan') {
            steps {
                sh './gradlew dependencyCheckAnalyze' 
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
                sh 'scp build/libs/my-app.jar ec2-user@staging-server:/path/to/deploy' 
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh './gradlew integrationTest' 
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'scp build/libs/my-app.jar ec2-user@production-server:/path/to/deploy' 
            }
        }
    }
}

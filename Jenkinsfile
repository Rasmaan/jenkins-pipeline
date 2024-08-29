pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package' // or your build command
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh 'mvn test' // or your testing command
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'mvn sonar:sonar' // or your code analysis command
            }
        }
        stage('Security Scan') {
            steps {
                sh 'dependency-check.sh --project my-app' // or your security scan command
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'scp target/my-app.jar ec2-user@staging-server:/path/to/deploy' // or your deploy command
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'run-staging-tests.sh' // or your staging tests command
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'scp target/my-app.jar ec2-user@production-server:/path/to/deploy' // or your deploy command
            }
        }
    }
    post {
        always {
            mail to: 'developer@example.com',
                 subject: "Pipeline Status: ${currentBuild.currentResult}",
                 body: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) finished with status: ${currentBuild.currentResult}. Check logs for details."
        }
    }
}

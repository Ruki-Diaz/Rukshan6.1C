pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example: Use Maven for Java projects
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example: Use JUnit or similar tools
                // sh 'mvn test'
            }
            post {
                always {
                    emailext(
                        to: 'dias.rukshan@gmail.com',
                        subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Check console output at ${env.BUILD_URL} to view the results.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                // Example: Use SonarQube or Checkstyle
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scans...'
                // Example: Use OWASP Dependency Check
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    emailext(
                        to: 'dias.rukshan@gmailcom',
                        subject: "Security Scan - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has ${currentBuild.currentResult}. Check console output at ${env.BUILD_URL} to view the results.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Example: Use AWS CLI for deployment
                // sh 'aws deploy...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example: Use test scripts specific to your environment
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Example: Use AWS CLI for production deployment
                // sh 'aws deploy...'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Tool: Maven' // Example build automation tool
                // sh 'mvn clean package' // Uncomment if actually running Maven
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Tools: JUnit for unit tests, Selenium for integration tests' // Example test automation tools
                // sh 'mvn test' // Uncomment if actually running tests
            }
            post {
                always {
                    emailext(
                        to: 'dias.rukshan@gmail.com',
                        subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Check the console output at ${env.BUILD_URL} to view the results.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality...'
                echo 'Tool: SonarQube' // Example code analysis tool
                // sh 'sonar-scanner' // Uncomment if actually running SonarQube
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scans...'
                echo 'Tool: OWASP Dependency Check' // Example security scanning tool
                // sh 'dependency-check.sh' // Uncomment if actually running a security scan
            }
            post {
                always {
                    emailext(
                        to: 'dias.rukshan@gmail.com',
                        subject: "Security Scan - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has ${currentBuild.currentResult}. Check the console output at ${env.BUILD_URL} to view the results.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo 'Tool: AWS CLI' // Example deployment tool
                // sh 'aws deploy...' // Uncomment if actually deploying to AWS
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'Tool: Selenium for integration tests on staging' // Example integration test tool
                // Use test scripts specific to your environment
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                echo 'Tool: AWS CLI' // Example deployment tool
                // sh 'aws deploy...' // Uncomment if actually deploying to production
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

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building project using Maven'
                // Add Maven build command
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Testing') {
            steps {
                echo 'Running unit test with JUnit'
                sh 'mvn test -Dtest=UnitTest'
                echo 'Running integration test using TestNG'
                sh 'mvn test -Dtest=IntegrationTest'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                    mail to: 'dias.rukshan@gmail.com',
                         subject: "Unit and Integration Testing - Success",
                         body: "The Unit and Integration Testing stage has passed."
                }
                failure {
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                    mail to: 'vinoj.prasath23@gmail.com',
                         subject: "Unit and Integration Testing - Failed",
                         body: "The Unit and Integration Testing stage has failed."
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis using SonarQube'
                // Add SonarQube scanner command
                sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Perform Security Scan using OWASP ZAP'
                // Add OWASP ZAP scan command
                sh 'zap-cli quick-scan --self-contained'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
                    mail to: 'dias.rukshan@gmail.com',
                         subject: "Security Scan - Success",
                         body: "The Security Scan stage has passed."
                }
                failure {
                    archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
                    mail to: 'dias.rukshan@gmail.com',
                         subject: "Security Scan - Failed",
                         body: "The Security Scan stage has failed."
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server AWS EC2'
                // Add deployment script/command for staging
                sh 'deploy-to-staging.sh'
            }
        }
        stage('Integration Test on Staging') {
            steps {
                echo 'Running integration tests on Staging'
                // Add commands to run integration tests on staging
                sh 'run-staging-tests.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production using AWS EC2'
                // Add deployment script/command for production
                sh 'deploy-to-production.sh'
            }
        }
    }
    post {
        always {
            mail to: 'dias.rukshan@gmail.com',
                 subject: "Pipeline Status",
                 body: "The pipeline has completed. Check the Jenkins console for details."
        }
    }
}

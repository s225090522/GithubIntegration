pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQubeServer'    // Set in Jenkins > Manage Jenkins > Configure System
        SONARQUBE_TOKEN = credentials('sonar-token')  // Add as Jenkins credentials (secret text)
        STAGING_SERVER = 'ec2-user@staging-server-ip' // Replace with actual IP
        PROD_SERVER = 'ec2-user@production-server-ip' // Replace with actual IP
    }

    triggers {
        pollSCM('H/5 * * * *') // Polls GitHub every 5 minutes
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building the project...'
               
            }
        }

        stage('Unit & Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
               
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis with SonarQube...'
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using Snyk...'
               
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
               
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
               
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Deploy to Production?', ok: 'Deploy'
                echo 'Deploying to production server...'
              
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

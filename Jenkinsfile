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
                sh 'mvn clean install' // Or use `npm install` for Node.js projects
            }
        }

        stage('Unit & Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test' // Or `npm test` or other test commands
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis with SonarQube...'
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh 'mvn sonar:sonar -Dsonar.login=$SONARQUBE_TOKEN'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using Snyk...'
                sh 'snyk test || true' // Avoid failing the pipeline, log results instead
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                sh """
                    ssh -o StrictHostKeyChecking=no $STAGING_SERVER 'bash -s' < deploy-staging.sh
                """
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                sh 'newman run postman_collection.json' // or use Selenium test runner
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Deploy to Production?', ok: 'Deploy'
                echo 'Deploying to production server...'
                sh """
                    ssh -o StrictHostKeyChecking=no $PROD_SERVER 'bash -s' < deploy-production.sh
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

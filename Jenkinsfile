pipeline {
    agent any

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
               {
                    
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

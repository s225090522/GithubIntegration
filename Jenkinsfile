pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Add build command here if needed
            }
        }

        stage('Unit & Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example: sh 'npm test' or sh './gradlew test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis with SonarQube...'
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh "sonar-scanner -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Running security scan using Snyk...'
                    try {
                        sh 'snyk test'
                    } catch (err) {
                        echo "Snyk scan failed: ${err}"
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Example: sh 'scp app.war user@staging:/apps'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
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
        failure {
            echo 'Pipeline failed!'
        }
    }
}



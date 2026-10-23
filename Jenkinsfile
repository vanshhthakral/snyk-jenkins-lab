pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('Snyk Dependency Scan') {
            steps {
                snykSecurity(
                    snykInstallation: 'Snyk-CLI',
                    snykTokenId: 'snyk-api-token',
                    failOnIssues: true,
                    severity: 'high',
                    additionalArguments: '--file=pom.xml'
                )
            }
        }
    }

    post {
        success {
            echo 'Build and security scan passed.'
        }
        failure {
            echo 'Pipeline failed: check build, tests, or security findings.'
        }
        always {
            echo 'CI/CD pipeline execution finished.'
        }
    }
}

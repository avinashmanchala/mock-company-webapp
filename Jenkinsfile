pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the application
                sh './gradlew assemble'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh './gradlew test'
            }
        }
    }

    post {
        always {
            // Archive test results and notify
            junit '**/build/test-results/test/*.xml'
            echo 'Build and test stages completed.'
        }
        failure {
            echo 'Build or tests failed. Please review the logs.'
        }
    }
}

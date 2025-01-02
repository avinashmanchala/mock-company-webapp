pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Frontend Build') {
            steps {
                sh '''
                # Use a specific Node.js version
                nvm install 18
                nvm use 18

                # Navigate to the frontend and build it
                cd client-app
                yarn install
                yarn build
                '''
            }
        }

        stage('Backend Build') {
            steps {
                sh './gradlew assemble'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml'
        }
        failure {
            echo 'Build or tests failed. Please review the logs.'
        }
    }
}

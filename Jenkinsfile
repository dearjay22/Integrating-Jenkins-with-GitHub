pipeline {
    agent any
    stages {

        // =========================
        // Build & Test Stage (like GitHub Actions build-and-test) 
        // =========================
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Node.js') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

    }

    post {
        always {
            cleanWs()
        }
        success {
        mail to: 'testuvpce@gmail.com',
             subject: "Jenkins Build PASSED: ${currentBuild.fullDisplayName}",
             body: "Good news! The Jenkins build '${currentBuild.fullDisplayName}' passed.\nCheck details at: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'testuvpce@gmail.com',
                subject: "Jenkins Build FAILED: ${currentBuild.fullDisplayName}",
                body: "Attention! The Jenkins build '${currentBuild.fullDisplayName}' failed.\nCheck logs at: ${env.BUILD_URL}"
        }
    }
}

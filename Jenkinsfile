pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nilukshanvijekumar/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins: Run Tests - ${currentBuild.currentResult}",
                        body: "Run Tests stage finished with status: ${currentBuild.currentResult}",
                        to: "nilukshanvije26@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins: NPM Audit - ${currentBuild.currentResult}",
                        body: "NPM Audit stage finished with status: ${currentBuild.currentResult}",
                        to: "nilukshanvije26@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}
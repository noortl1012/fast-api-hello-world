pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                // Install pytest (and other dependencies if needed)
                bat 'pip install pytest'
            }
        }
        stage('Run Tests') {
            steps {
                // Run pytest
                bat 'pytest'
            }
        }
        stage('Code Analysis') {
            environment {
                scannerHome = tool 'Sonar'
            }
            steps {
                script {
                    withSonarQubeEnv('Sonar') {
                        bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" \
                            -Dsonar.projectKey=fast-api-sonar \
                            -Dsonar.projectName=fast-api-sonar"
                    }
                }
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                // Install pytest (and other dependencies if needed)
                sh 'pip install pytest'
            }
        }
        stage('Run Tests') {
            steps {
                // Run pytest
                sh 'pytest'
            }
        }
        stage('Code Analysis') {
            environment {
                scannerHome = tool 'Sonar'
            }
            steps {
                script {
                    withSonarQubeEnv('Sonar') {
                        sh "${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=fast-api-sonar \
                            -Dsonar.projectName=fast-api-sonar \
                            "
                    }
                }
            }
        }
    }
}

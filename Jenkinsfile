pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                // Install pytest (and other dependencies if needed)
                bat 'pip install pytest'
            }
        }
        // stage('Run Tests') {
        //     steps {
        //         // Run pytest
        //         bat 'pytest'
        //     }
        // }
        stage('Code Analysis') {
            steps {
                dir("${WORKSPACE}") {
                    // Run SonarQube analysis for Python
                    script {
                        def scannerHome = tool name: 'scanner-name', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        withSonarQubeEnv('sq1') {
                            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" \
                                -Dsonar.projectKey=fast-api-sonar \
                                -Dsonar.projectName=fast-api-sonar"
                        }
                    }
                }
            }
        }
    }
}

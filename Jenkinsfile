pipeline {
    agent any
    stages {
        stage('Verify JAVA_HOME') {
            steps {
                bat 'echo %JAVA_HOME%'
                bat 'dir %JAVA_HOME%\\bin'
            }
        }
        stage('Setup') {
            steps {
                bat 'pip install pytest'
            }
        }
        stage('Code Analysis') {
            steps {
                dir("${WORKSPACE}") {
                    script {
                        def scannerHome = tool name: 'sq1', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        withSonarQubeEnv('sq1') {
                            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" -Dsonar.projectKey=fast-api-sonar -Dsonar.projectName=fast-api-sonar"
                        }
                    }
                }
            }
        }
    }
}

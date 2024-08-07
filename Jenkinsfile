node {
  stage('SCM') {
    checkout scm
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
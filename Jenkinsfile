pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your SCM (e.g., Git)
                git 'https://github.com/your/repository.git'
            }
        }
        stage('Setup') {
            steps {
                // Install dependencies
                sh '''
                python -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                // Run tests
                sh '''
                . venv/bin/activate
                pytest --junitxml=test-results.xml
                '''
            }
            post {
                always {
                    junit 'test-results.xml'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    . venv/bin/activate
                    sonar-scanner \
                    -Dsonar.projectKey=your_project_key \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://192.168.1.20:9000 \
                    -Dsonar.login=sonar_creds
                    '''
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}


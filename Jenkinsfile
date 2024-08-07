pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("fastapi-hello-world")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'echo "Running tests..."'
                        sh 'curl http://localhost:80'
                    }
                }
            }
        }
    }
}

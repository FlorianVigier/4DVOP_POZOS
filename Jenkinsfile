pipeline {
    agent { ./App_Server/simple_api/dockerfile true }
    stages {
        stage('Build') {
            steps {
                echo 'Building docker image from Dockerfile'
            }
            step {
                echo 'Running docker image'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if the apps works well'
            }
        }
        stage('Scan') {
            steps {
                echo 'Test app vulnerability through clair scanner tool'
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing the image to the registry'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Secure') {
            steps {
                echo 'Testing trough Arachni tool'
            }
        }
    }
}

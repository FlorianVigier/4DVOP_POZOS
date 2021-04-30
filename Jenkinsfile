pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building and Running ocker image from Dockerfile'
                sh "docker build -t flask ."
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

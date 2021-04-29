pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
            dir '/App_Server/simple_api'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building and running docker image from Dockerfile'
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

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building and Running ocker image from Dockerfile'
                echo '------------------------------------------------'
                sh "docker build -t flask ."
                sh "docker run -d -p 5000:5000 --name flask flask"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if the apps works well'
                echo '------------------------------'
                sh 'curl -u toto:python -X GET http://0.0.0.0:5000/pozos/api/v1.0/get_student_ages'
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
        stage('Clean') {
            steps {
                sh 'docker stop flask' 
                sh 'docker rm flask'
            }
        }
    }
}

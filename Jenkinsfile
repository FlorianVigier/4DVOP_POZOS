pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building and Running ocker image from Dockerfile'
                sh "docker build -t flask ."
                sh "docker run -d -p 5000:5000 --name flask flask"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if the apps works well'
                sh 'curl -u toto:python -X GET http://0.0.0.0:5000/pozos/api/v1.0/get_student_ages'
            }
        }
        stage('Scan') {
            steps {
                echo 'Test app vulnerability through clair scanner tool'
                sh 'docker run -d --name db arminc/clair-db'
                sh 'sleep 15'

                sh 'docker run -p 6060:6060 --link db:postgres -d --name clair arminc/clair-local-scan'
                sh 'sleep 1'

                sh 'DOCKER_GATEWAY=$(docker network inspect bridge --format "{{range .IPAM.Config}}{{.Gateway}}{{end}}")
                wget -qO clair-scanner https://github.com/arminc/clair-scanner/releases/download/v8/clair-scanner_linux_amd64 && chmod +x clair-scanner 
                ./clair-scanner --ip="$DOCKER_GATEWAY" flask || exit 0'
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

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building and Running docker image from Dockerfile'
                sh 'docker stop flask || exit 0'
                sh 'docker rm flask || exit 0'

                sh "docker build -t flask ."
                sh "docker run -d -p 5000:5000 --name flask flask"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if the app work well'
                sh 'sleep 5'
                sh 'curl -u toto:python -X GET http://0.0.0.0:5000/pozos/api/v1.0/get_student_ages'
            }
        }
        stage('Scan') {
            steps {
                sh 'docker stop db || exit 0'
                sh 'docker rm db || exit 0'
                
                sh 'docker stop clair || exit 0'
                sh 'docker rm clair || exit 0'
                
                echo 'Test app vulnerability through clair scanner tool'
                echo 'Running database'

                sh 'docker run -d --name db arminc/clair-db'
                sh 'sleep 10'

                echo 'Running clair scanner'

                sh 'docker run -p 6060:6060 --link db:postgres -d --name clair arminc/clair-local-scan'
                sh 'sleep 5'

                echo 'Running clair scan'

                sh 'DOCKER_GATEWAY=$(docker network inspect bridge --format "{{range .IPAM.Config}}{{.Gateway}}{{end}}")'

                sh 'wget -qO clair-scanner https://github.com/arminc/clair-scanner/releases/download/v8/clair-scanner_linux_amd64 && chmod +x clair-scanner'
                sh './clair-scanner --ip="$DOCKER_GATEWAY" flask || exit 0'
            
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
                echo 'Clean'
                sh 'docker stop flask || exit 0' 
                sh 'docker rm flask || exit 0'
                sh 'docker stop db || exit 0'
                sh 'docker rm db || exit 0'
                sh 'docker stop clair || exit 0'
                sh 'docker rm clair || exit 0'
            }
        }
    }
}

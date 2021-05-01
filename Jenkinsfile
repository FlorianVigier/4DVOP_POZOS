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
                echo 'Testing if the app work well'
                sh 'sleep 5'
                sh 'curl -u toto:python -X GET http://0.0.0.0:5000/pozos/api/v1.0/get_student_ages'
            }
        }
        stage('Scan') {
            steps {
                echo 'Test app vulnerability through clair scanner tool'
                echo 'Running database'

                sh 'docker run -d --name db arminc/clair-db'
                sh 'sleep 10'

                echo 'Running clair scanner'

                sh 'docker run -p 6060:6060 --link db:postgres -d --name clair arminc/clair-local-scan'
                sh 'sleep 1'

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
                /*sh 'docker stop flask' 
                sh 'docker rm flask'*/
            }
        }
    }
}

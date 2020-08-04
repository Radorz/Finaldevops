pipeline {
    agent {
        docker {
            image 'node:10-alpine'
            args '-p 4040:4040'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
               sh 'chmod +x ./jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh 'npm run build && npm start'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'chmod +x ./jenkins/scripts/kill.sh'
            }
        }
    }
}

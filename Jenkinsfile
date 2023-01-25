pipeline {
    agent {
        docker {
            image 'node:lts-bullseye-slim' 
            args '-p 3000:3000'
        }
    }
    environment {
        HOME = '.'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo "Test stage"
            }
        }
        stage('Deliver') {
            steps {
                set -x
                sh 'npm run build'
                set +x
                sh 'npm start &'
                sleep 1
                set +x
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './public/kill.sh'
            }
        }
    }
}

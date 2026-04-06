pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                bat 'start conference.html'
            }
        }

        stage('Run') {
            steps {
                bat 'python -m http.server 8000'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '*.class', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Mini CI: SUCCESS - artifacts archived'
        }
        failure {
            echo 'Mini CI: FAILURE - check compilation errors'
        }
    }
}

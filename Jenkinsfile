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
                bat 'javac Hello.java'
            }
        }

        stage('Run') {
            steps {
                bat 'java Hello'
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

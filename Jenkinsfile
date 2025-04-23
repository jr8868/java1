pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/jr8868/java1'
            }
        }

        stage('Build') {
            steps {
                 bat 'start gradlew build'
            }
        }

        stage('Test') {
            steps {
                bat 'start gradlew test'
            }
        }

        stage('Deploy') {
            steps {
                powershell 'java -jar build/libs/hello-world-javaV1.jar'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir()
        }

        success {
            echo 'Build succeeded!!!'
            archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            junit 'build/test-results/test/*.xml'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
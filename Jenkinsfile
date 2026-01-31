pipeline {
    agent any
    environment {
        PATH = "/opt/gradle-8.5/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                sh 'gradle clean build'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh 'gradle sonar'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

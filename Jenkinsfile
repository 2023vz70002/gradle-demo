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
                // Changed from 'test' to 'build' to ensure JAR creation
                sh 'gradle clean build'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

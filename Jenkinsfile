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
                // Passing the token directly via command line to ensure authorization
                sh 'gradle sonar -Dsonar.token=squ_b2e37ac9fa5c31bafec71f7ec0ed84382b930ea4'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

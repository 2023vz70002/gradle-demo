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
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    // We use the variable SONAR_TOKEN provided by Jenkins
                    sh "gradle sonar -Dsonar.token=${SONAR_TOKEN}"
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

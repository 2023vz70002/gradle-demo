pipeline {
    agent any
    environment {
        PATH = "/opt/gradle-8.5/bin:$PATH"
        // This securely pulls the secret we just created in Jenkins
        SONAR_AUTH_TOKEN = credentials('SONAR_TOKEN')
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
                // Using the environment variable to pass the token
                sh "gradle sonar -Dsonar.token=${SONAR_AUTH_TOKEN}"
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

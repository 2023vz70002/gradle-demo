pipeline {
    agent any
    environment {
        // Explicitly adding Gradle path to Jenkins environment
        PATH = "/opt/gradle-8.5/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                // Pulls source code from GitHub
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                // Executes build and test stages
                sh 'gradle clean test'
            }
        }
        stage('Archive Artifact') {
            steps {
                // Archives the JAR file for Jenkins UI download
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
            }
        }
    }
}

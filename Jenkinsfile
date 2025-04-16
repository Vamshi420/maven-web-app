pipeline {
    agent any

    tools {
        maven 'maven-3.9.9' // Make sure this name matches Jenkins' Global Tool Configuration
    }

    environment {
        PATH = "${PATH}:/opt/maven/bin"
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/Vamshi420/maven-web-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=01-maven-web-app'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
}

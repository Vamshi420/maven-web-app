pipeline {
    agent any

    tools {
        maven 'maven-3.9.9'  // Make sure this matches Jenkins Global Tool Configuration
    }

    environment {
        PATH = "$PATH:/opt/maven/bin"
    }

    stages {
        stage('Checkout Code') {
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
                    sh 'mvn sonar:sonar'
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
}

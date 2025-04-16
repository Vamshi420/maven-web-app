pipeline {
    agent any

    environment {
        PATH = "$PATH:/opt/maven/bin"
    }

    tools {
        maven 'Maven3.9.9'  // Make sure "Maven3" is configured in Jenkins Global Tool Configuration
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
                withSonarQubeEnv('sonarqube') { // 'sonarqube' must match your Jenkins SonarQube server name
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}

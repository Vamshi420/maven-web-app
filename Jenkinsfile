pipeline {
    agent any

    environment {
        PATH = "$PATH:/opt/maven/bin"
    }

    tools {
        maven 'maven-3.9.9' // ✅ Must match exactly with your Jenkins tool name
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Vamshi420/maven-web-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') { // ✅ Must match Jenkins Sonar config name
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }    
}

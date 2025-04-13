pipeline {
    agent any

    tools {
        maven 'maven' // 👈 this should match your Jenkins Maven tool name
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Vamshi420/maven-web-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Replace with actual deployment logic
                sh 'cp target/*.war /path/to/tomcat/webapps/'
            }
        }
    }
}


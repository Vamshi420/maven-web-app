pipeline {
    agent any

    tools {
        maven 'maven'         // Change as per your Maven installation name
        jdk 'java17'                // Change as per your JDK installation name
    }

    environment {
        GIT_REPO = 'https://github.com/Vamshi420/maven-web-app.git'  // Replace with your repo
        TOMCAT_URL = 'http://3.109.54.9:8080/'                      // Tomcat IP and port
        DEPLOY_CONTEXT = 'maven-web-app.war'                                            // Context path ('' means ROOT)
        CREDENTIALS_ID = 'tomcat'                                // Jenkins credentials ID
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                git url: "${github.com/Vamshi420/maven-web-app.git}"
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(credentialsId: "${tomcat}", 
                            path: "${DEPLOY_CONTEXT}", 
                            url: "${http://3.109.54.9:8080/}")
                ], 
                contextPath: "${DEPLOY_CONTEXT}", 
                war: 'target/maven-web-app.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed. Check logs for more info.'
        }
    }
}

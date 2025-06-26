pipeline {
    agent any

    tools {
        maven 'maven'     // Replace with your Maven name in Jenkins
        jdk 'java17'            // Replace with your JDK name in Jenkins
    }

    environment {
        GIT_REPO = 'https://github.com/VamshiM123/maven-web-app.git'  // Update if needed
        TOMCAT_URL = 'http://3.109.54.9:8080'                          // Tomcat server
        DEPLOY_CONTEXT = ''                                           // '' means deploy to root
        CREDENTIALS_ID = 'tomcat-cred'                                // Jenkins credentials ID
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                git url: "${GIT_REPO}"
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
                    tomcat9(
                        credentialsId: "${CREDENTIALS_ID}",
                        path: "${DEPLOY_CONTEXT}",
                        url: "${TOMCAT_URL}"
                    )
                ],
                contextPath: "${DEPLOY_CONTEXT}",
                war: 'target/maven-web-app.war'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully.'
        }
        failure {
            echo '❌ Deployment failed. Check console output for details.'
        }
    }
}

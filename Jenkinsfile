pipeline {
    agent any

    tools {
        maven 'maven'        // Ensure Maven3 is configured in Jenkins global tools
        jdk 'java17'           // Make sure jdk17 is installed and configured in Jenkins
    }

    environment {
        GIT_REPO = 'https://github.com/Vamshi420/maven-web-app.git' // Updated repo
    }

    stages {
        stage('Checkout') {
            steps {
                git url: "${GIT_REPO}", branch: 'master'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn clean verify sonar:sonar -Dsonar.token=$SONAR_TOKEN'
                    }
                }
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASS')]) {
                    sh '''
                        echo "Deploying to Tomcat..."
                        curl -T target/*.war http://$TOMCAT_USER:$TOMCAT_PASS@15.207.14.236:8080/manager/text/deploy?path=/myapp&update=true
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build, Sonar Scan, and Deployment succeeded!'
        }
        failure {
            echo '❌ Something went wrong. Check logs above.'
        }
    }
}

pipeline {
    agent any

    tools {
        maven 'maven'  // Make sure 'maven' is configured in Jenkins > Global Tool Configuration
    }

    environment {
        SONAR_URL = 'http://43.204.218.218:9000'
        SONAR_LOGIN = credentials('sonar-token') // Add your token in Jenkins Credentials as 'sonar-token'
        TOMCAT_URL = 'http://15.207.14.236:8080/manager/text/deploy?path=/maven-web-app&update=true'
        TOMCAT_CRED = credentials('tomcat-credentials') // Add tomcat username/password in Jenkins Credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Vamshi420/maven-web-app.git', branch: 'master'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=$SONAR_LOGIN'
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
                script {
                    def warFile = 'target/maven-web-app.war'
                    sh """
                        curl -v --fail -u $TOMCAT_CRED_USR:$TOMCAT_CRED_PSW --upload-file $warFile "$TOMCAT_URL"
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful.'
        }
        failure {
            echo '❌ Something went wrong. Check logs above.'
        }
    }
}

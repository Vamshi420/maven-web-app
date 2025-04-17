pipeline {
    agent any

    environment {
        MAVEN_HOME = '/opt/maven'
        JAVA_HOME = '/usr/lib/jvm/java-17-amazon-corretto.x86_64'
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin123'
        TOMCAT_URL = 'http://52.66.203.33:8080/:8080/manager/text/deploy?path=/maven-web-app&update=true'
    }

    tools {
        maven 'maven' // Make sure this is configured in Jenkins (Global Tool Configuration)
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                git url: 'https://github.com/Vamshi420/maven-web-app.git', branch: 'master'
            }
        }

        stage('Build with maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    curl -v --fail -u $TOMCAT_USER:$TOMCAT_PASS \
                    --upload-file target/maven-web-app.war \
                    "$TOMCAT_URL"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build & deployment successful!'
        }
        failure {
            echo '❌ Something went wrong. Check logs above.'
        }
    }
}

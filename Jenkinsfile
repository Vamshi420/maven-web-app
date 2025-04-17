pipeline {
    agent any

    environment {
        MAVEN_HOME = '/opt/maven'
        JAVA_HOME = '/usr/lib/jvm/java-17-amazon-corretto.x86_64'
    }

    tools {
        maven 'maven' // Replace 'MAVEN' with your Maven tool name in Jenkins config
    }

    stages {
        stage('Checkout from Git') {
            steps {
                git url: 'https://github.com/Vamshi420/maven-web-app.git', branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'admin', passwordVariable: 'admin123')]) {
                    sh '''
                        curl -v --fail -u $TOMCAT_USER:$TOMCAT_PASS \
                        --upload-file target/maven-web-app.war \
                        "http://localhost:8080/manager/text/deploy?path=/maven-web-app&update=true"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}

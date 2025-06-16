pipeline {
    agent any

    environment {
        MAVEN_HOME = tool '/opt/maven' // Jenkins Maven tool name
    }

    stages {
        stage('Clone from Git') {
            steps {
                git url: 'https://github.com/Vamshi420/maven-web-app.git', branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(credentialsId: 'tomcat-credentials', 
                            path: '', 
                            url: 'http://15.207.117.205:8080/manager/text')
                ], 
                contextPath: 'yourapp', 
                war: '**/target/*.war'
            }
        }
    }
}

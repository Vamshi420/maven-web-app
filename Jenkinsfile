pipeline {
    agent any

    tools {
        maven 'maven' // Make sure this is set in Jenkins Global Tool Config
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

        stage('Deploy') {
            steps {
                sh 'cp target/*.war /opt/tomcat/webapps/' // Make sure Jenkins has access
            }
        }
    }
}

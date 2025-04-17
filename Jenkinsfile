pipeline {
    agent any
    environment {
        TOMCAT_URL = 'http://52.66.203.33:8080/manager/text/deploy?path=/maven-web-app&update=true'
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin123'
    }
    stages {
        stage('Clone from GitHub') {
            steps {
                git 'https://github.com/Vamshi420/maven-web-app.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy WAR file to Tomcat
                    def deployUrl = TOMCAT_URL
                    def deployCmd = """
                        curl -v --fail -u $TOMCAT_USER:$TOMCAT_PASS --upload-file target/maven-web-app.war "$deployUrl"
                    """
                    sh deployCmd
                }
            }
        }
    }
    post {
        always {
            echo 'Build and deploy pipeline completed.'
        }
        failure {
            echo '❌ Something went wrong. Check logs above.'
        }
    }
}

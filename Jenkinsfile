pipeline {
    agent any
    environment {
        TOMCAT_URL = 'http:/15.207.117.205:8080/manager/text/deploy?path=/maven-web-app&update=true'
        TOMCAT_USER = 'tomcat'
        TOMCAT_PASS = 'tomcat'
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
                    def deployUrl = http://15.207.117.205:8080/
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

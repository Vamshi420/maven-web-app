pipeline {
    agent any

    environment {
        MAVEN_HOME = '/opt/maven' // Change this if Maven is in a different path
        JAVA_HOME = '/usr/lib/jvm/java-17-amazon-corretto.x86_64' // Adjust if needed
    }

    tools {
        maven 'maven' // Name of Maven tool configured in Jenkins (Manage Jenkins → Global Tool Configuration)
    }

    stages {
        stage('Clone Repository') {
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
                script {
                    def warFile = 'target/maven-web-app.war'
                    def tomcatUrl = 'http://52.66.203.33:8080//manager/text/deploy?path=/maven-web-app&update=true'

                    withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'admin', passwordVariable: 'admin123')]) {
                        sh """
                            curl -u $TOMCAT_USER:$TOMCAT_PASS --upload-file $warFile "$tomcatUrl"
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}

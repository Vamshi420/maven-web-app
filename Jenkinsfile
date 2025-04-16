pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/maven/bin"
    }
    stages{
        stage('getcode'){
            steps{
                git 'https://github.com/Vamshi420/maven-web-app.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('sonarqube-analysis') {
            steps {
                withsonarqubeEnv('sonarqube') {
                    sh "mvn sonar:sonar"
                }
            }
        }
}

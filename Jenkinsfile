pipeline {
    agent any
    tools {
        maven 'Maven 3.5.3'
        jdk 'jdk1.8.0_131'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
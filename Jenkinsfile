pipeline {
    agent any
    tools {
        maven 'localMaven'
        jdk 'localJDK'
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
        stage('Deploy to staging'){
            steps{
                build job: 'deploy-to-staging-by-package-pipeline'
            }
        }
        stage('Deploy to production'){
            steps{
                timeout(time:5, unit:"DAYS"){
                    input message: 'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-to-prod-by-package-pipeline'
            }
            post{
                success{
                    echo 'Code deployed to Production.'
                }

                failure{
                    echo 'Deploymeny failed.'
                }
            }
        }
    }
}
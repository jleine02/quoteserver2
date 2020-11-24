pipeline {
    agent any

    tools {nodejs "node"}

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit Tests') {
            steps {
              sh 'echo Running Unit Tests...'
              sh 'node /var/lib/jenkins/workspace/QuoteServerPipeline/serverside/testAllQuotes.js'
            }
        }
        stage('Deploy to Stage Env') {
            steps {
              sh 'echo Deploying to Stage...'
              sh '/var/lib/jenkins/workspace/QuoteServerPipeline/serverside/script/deployStage'
            }
        }
        stage('System Tests') {
            steps {
              sh 'echo Running System Tests...'
              input 'Deploy to Production?'
            }
        }
        stage('Deploy to Prod Env') {
            steps {
              sh 'echo Deploying to Production...'
              sh 'sudo /var/lib/jenkins/workspace/QuoteServerPipeline/serverside/script/deployProd'
            }
        }
    }
}

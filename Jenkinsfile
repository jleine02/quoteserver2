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
              sh 'echo Deploying to Stage'
              sh 'cd /var/lib/jenkins/workspace/QuoteServerPipeline/serverside'
              sh './script/deploy'
            }
        }
    }
}

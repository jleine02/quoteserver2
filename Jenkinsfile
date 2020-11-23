pipeline {
    agent any

    tools {nodejs "node"}

    stages {
        stage('Build') {
            steps {
                sh 'echo Running Unit Tests...'
                sh 'npm install -g'
            }
        }
        stage('Unit Tests') {
            steps {
              sh 'cd /var/lib/jenkins/workspace/QuoteServerPipeline/serverside'
              sh 'node testAllQuotes.js'
            }
        }
        stage('Deploy to Stage Env') {
            steps {
              sh 'echo Deploying to Stage'
              sh './script/deploy'
            }
        }
    }
}

pipeline {
    agent any

    tools {nodejs "node"}

    stages {
        stage('Build') {
            steps {
                sh 'echo Running Unit Tests...'
                sh 'npm install'
            }
        }
        stage('Unit Tests') {
            steps {
              sh 'node /var/lib/jenkins/workspace/QuoteServerPipeline/ /
              serverside/testAllQuotes.js'
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

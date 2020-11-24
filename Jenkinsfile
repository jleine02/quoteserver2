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
              sh 'id -a'
              sh '''
                su - leiner
                cd /home/leiner


                # Get the current production server and
                # set TARGET to the other server
                sudo doctl auth init --access-token "7743031e82923852c7a305f9de2ccd72bca99d7e686381033d3cf4f638cf87ff"
                CURRENT=$(curl -s http://161.35.252.207:3001/hostname)
                if [ "$CURRENT" = "blue-production" ]; then
                  TARGET="165.22.2.7"
                  echo "Promoting stage env to prod at ip address " $TARGET " on port 3001"
                  sudo doctl compute floating-ip-action assign 161.35.252.207 217997548 --context jenkins
                elif [ "$CURRENT" = "green-production" ]; then
                  TARGET="142.93.193.167"
                  echo "Promoting stage env to prod at ip address " $TARGET " on port 3001"
                  sudo doctl compute floating-ip-action assign 161.35.252.207 218158847 --context jenkins
                else
                  echo "Something is not right! 😬"
                  exit -1
                fi

                CURRENT=$(curl -s http://161.35.252.207:3001/hostname)
                echo "Current deployment is now" $CURRENT "on port 3001"
              '''
            }
        }

    }
}

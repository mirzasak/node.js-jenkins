pipeline {
    agent any
    stages {
        stage('Code') {
            steps {
                git url: 'https://github.com/mirzasak/node.js-jenkins', branch: 'main'
            }
        }
      stage('SSH Connect'){
          sshagent(['jenkins_ssh_key']) {
            sh 'ssh ubuntu@3.81.134.252'
          }
      }
        stage('Deploy') {
            steps {
                    sh ''' 
                        git config --global --add safe.directory /home/ubuntu/node.js-jenkins
                        cd /home/ubuntu/node.js-jenkins/
                        git add .
                        git commit -m "Save local changes before pulling"
                        git pull origin main --rebase
                        npm install
                        pm2 restart index.js --name testjs1
                    '''
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Code') {
            steps {
                git url: 'https://github.com/mirzasak/node.js-jenkins', branch: 'main'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['jenkins_ssh_key']) {
                    sh '''
                        ssh ubuntu@3.81.134.252 "
                            cd /home/ubuntu/node.js-jenkins
                            git config --global --add safe.directory /home/ubuntu/node.js-jenkins
                            git add .
                            git commit -m 'Save local changes before pulling' || echo 'No changes to commit'
                            git pull origin main --rebase
                            npm install
                            pm2 restart index.js --name testjs1
                        "
                    '''
                }
            }
        }
    }
}

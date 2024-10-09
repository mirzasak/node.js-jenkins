pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // GitHub'dan projeyi klonla
                git branch: 'main', url: 'https://github.com/mirzasak/node.js-jenkins'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no -i $SSH_KEY ubuntu@54.204.153.38 '
                            cd /home/ubuntu/node.js-jenkins
                            git pull origin main
                            npm install
                            pm2 restart index.js --name test2
                        '
                    '''
                }
            }
        }
    }
}

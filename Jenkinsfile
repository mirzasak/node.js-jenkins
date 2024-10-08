pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/mirzasak/node.js-jenkins.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['jenkins_ssh_key']) { // Daha önce eklediğiniz credential ID
                    sh '''
                        ssh ubuntu@3.81.134.252 "cd /home/ubuntu/node.js-jenkins && npm install && pm2 restart index.js"
                    '''
                }
            }
        }
        //stage('Deploy to EC2') {
          //  steps {
           //     withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_ssh_key', keyFileVariable: 'SSH_KEY')]) {
             //       sh '''
               //         # ssh-keyscan -H <EC2_PUBLIC_IP> >> ~/.ssh/known_hosts
                 //       ssh -o StrictHostKeyChecking=no -i $SSH_KEY ubuntu@3.81.134.252 '
                   //         cd /home/ubuntu/node.js-jenkins # || mkdir -p /home/ubuntu/node.js-jenkins
                     //       git config --global --add safe.directory /home/ubuntu/node.js-jenkins
                         //   git clone https://github.com/mirzasak/node.js-jenkins.git . || (git pull origin main)
                         //   npm install
                           // pm2 restart index.js --name testjs1 || pm2 start index.js --name testjs1
                       // '
                    //'''
               // }
           // }
       // }
    }
}

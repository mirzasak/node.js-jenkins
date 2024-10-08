pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // GitHub'dan projeyi klonla
                git branch: 'main', url: 'https://github.com/mirzasak/node.js-jenkins'
            }
        }

        stage('Install Dependencies') {
            steps {
                // EC2'de projeyi çalıştırmadan önce gerekli bağımlılıkları yükle
                sshagent(credentials: ['ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@35.173.212.106 <<EOF
                    cd /home/ubuntu/
                    git pull origin main
                    npm install
                    EOF
                    '''
                }
            }
        }

        stage('Restart Application') {
            steps {
                // Node.js uygulamasını PM2 veya systemd kullanarak yeniden başlat
                sshagent(credentials: ['ssh-key']) {
                    sh '''
                    ssh ubuntu@35.173.212.106 <<EOF
                    cd /home/ubuntu    
                    pm2 stop all || true
                    pm2 start index.js
                    EOF
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
            failure {
                echo 'Deployment failed!'
        
            }
        }
    }    

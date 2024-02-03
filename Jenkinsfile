pipeline {
    agent any

    stages {
        stage('Update EC2'){
            steps{
                sshagent(credentials : ['hero-vired-credentials']) {
                    sh'''
                    ssh -o StrictHostKeyChecking=no ${SSH_USER}@${SERVER_IP} '
                        sudo apt update
                        sudo apt install nginx -y
                    '
                     '''
                }
                
            }
        }
        stage('Replace html for nginx') {
            steps {
                sshagent(credentials : ['hero-vired-credentials']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ${SSH_USER}@${SERVER_IP} '
                            
                            sudo cp index.html /var/www/html
                        '
                    '''
                }
                
               
                        
                    
            }
        }
        stage('Copying configuration and restarting nginx'){
            steps{
                sshagent(credentials : ['hero-vired-credentials']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ${SSH_USER}@${SERVER_IP} '
                            sudo echo -e "server{server_name index;root /var/www/html;location / {index index.html;}}
                            sudo systemctl restart nginx
                        '
                    '''
                }
            }
                
                
            
        }
    }
}

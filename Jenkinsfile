pipeline {
    
    agent none

    stages {
        stage('Git clone') {
            agent { label 'agent-lftp' }
            steps {
                git branch: 'main', url: 'https://github.com/sylvainferrer/TP_Frontend_deployment_cda.git'
            }
        }
        stage('Copy server') {
            agent { label 'agent-lftp' }
            steps {
                sh '''
                   lftp -u hoopstore,'Azerty77380' ftp-hoopstore.alwaysdata.net -e "mirror -R ${WORKSPACE}/ www/ ; quit"
                '''
            }
        }
        stage('Npm') {
            agent { label 'agent-node' }
                steps {
                     sh '''
                        sshpass -p "Azerty77380" ssh -o StrictHostKeyChecking=no hoopstore@ssh-hoopstore.alwaysdata.net '
                        cd www/ &&
                        npm install
                        '
                    '''
                }
        }
        stage('Modifier .env') {
            agent { label 'agent-node' }
            steps {
                script {
                    sh '''
                    sshpass -p "Azerty77380" ssh -o StrictHostKeyChecking=no hoopstore@ssh-hoopstore.alwaysdata.net "
                        echo 'API_URL=http://storehoop.alwaysdata.net/api/podcast.php' > www/.env
                    "
                    '''
                }
            }
        }
    }
}

pipeline {
    
    agent none

    stages {
        stage('Git clone') {
            agent { label 'agent-node' }
            steps {
                git branch: 'main', url: 'https://github.com/sylvainferrer/TP_Frontend_deployment_cda.git'
            }
        }
         stage('quality check') {
            steps {
                sh '''
                   sonar-scanner \
  -Dsonar.projectKey=Sylvain_TP_Front \
  -Dsonar.sources=. \
  -Dsonar.host.url=https://669b-212-114-26-208.ngrok-free.app \
  -Dsonar.token=sqp_df478fd8681ddd718af33b3dc8358d5b2b1d5f5f
                '''
            }
        }
        stage('Copy server') {
            agent { label 'agent-node' }
            steps {
                sh '''
                   lftp -u hoopstore,"$Mdp" "$ftp" -e "mirror -R ${WORKSPACE}/ www/ ; quit"
                '''
            }
        }
        stage('Npm') {
            agent { label 'agent-node' }
                steps {
                     sh '''
                        sshpass -p "$Mdp" ssh -o StrictHostKeyChecking=no "$ssh" '
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
                    sshpass -p "$Mdp" ssh -o StrictHostKeyChecking=no "$ssh" "
                        echo 'API_URL=http://storehoop.alwaysdata.net/api/podcast.php' > www/.env
                    "
                    '''
                }
            }
        }
    }
}

pipeline {
    agent any

    environment {
        GIT_EC2 = "ubuntu@35.90.63.121"
        REMOTE_REPO_PATH = "/home/ubuntu/new/" // adjust this if your Git repo path is different
        LOCAL_DEPLOY_PATH = "/var/www/html"
    }

    stages {
        stage('Clone from Git EC2') {
            steps {
                sshagent(['jenkins-ssh-key']) {
                    sh '''
                        rm -rf temp_repo
                        ssh -o StrictHostKeyChecking=no $GIT_EC2 "tar -czf - -C $REMOTE_REPO_PATH ." | tar -xzf - -C .
                        mkdir -p temp_repo
                        mv * temp_repo || true
                    '''
                }
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh '''
                    sudo rm -rf $LOCAL_DEPLOY_PATH/*
                    sudo cp -r temp_repo/* $LOCAL_DEPLOY_PATH/
                    sudo systemctl reload nginx
                '''
            }
        }
    }
}

pipeline {
    agent any

    environment {
        GIT_EC2 = "ubuntu@35.90.63.121"
        REMOTE_REPO_PATH = "/home/ubuntu/new/"
        LOCAL_DEPLOY_PATH = "/var/www/html"
    }

    stages {
        stage('Clone from Git EC2') {
    steps {
        sshagent(['jenkins-ssh-key1']) {
            sh '''
                rm -rf temp_repo
                ssh -o StrictHostKeyChecking=no $GIT_EC2 "tar -czf - -C $REMOTE_REPO_PATH ." | tar -xzf - -C .
                mkdir -p temp_repo
                bash -c "shopt -s extglob && mv !(temp_repo) temp_repo"
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

pipeline {
    agent any

    environment {
        LOCAL_DEPLOY_PATH = "/var/www/html"
    }

    stages {
        stage('Deploy Travel Website to Nginx') {
            steps {
                sh '''
                    sudo rm -rf $LOCAL_DEPLOY_PATH/*
                    sudo cp -r Travel/* $LOCAL_DEPLOY_PATH/
                    sudo systemctl reload nginx
                '''
            }
        }
    }
}

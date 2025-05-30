pipeline {
    agent any

    environment {
        LOCAL_DEPLOY_PATH = "/var/www/html"
    }

    stages {
        stage('Deploy to Nginx') {
            steps {
                sh '''
                    sudo rm -rf $LOCAL_DEPLOY_PATH/*
                    sudo cp -r * $LOCAL_DEPLOY_PATH/
                    sudo systemctl reload nginx
                '''
            }
        }
    }
}

pipeline {
    agent any // window agent, Jenkins-laravel (other machine)
     environment {
        BOT_TOKEN = "6829228753:AAHg_B5JT9DJxCmQYskzWl4eSUvslvww-cA"
        CHAT_ID = "-1001840170075"
    }

    stages {
        stage('Fetch from GitHub') { //build steps
            steps {
                echo 'Fetching for GitHub'
                git branch: 'TP03' , url: 'https://github.com/pin-seavmuy/Jenkins.git'
            }
        }
        stage('Composer install') { 
            steps {
                sh 'composer install'
            }
        }
        stage('Copy .env') { 
            steps {
                sh 'cp .env.example .env'
            }
        }
        stage('Add key') { 
            steps {
                echo 'running code ...'
                sh 'php artisan key:generate'
            }
        }
        stage('npm') { 
            steps {
                echo 'Compiling code ...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test the app'){
            steps{
                echo 'Testing unit tests...'
                echo 'Testing feature...'
                sh 'php artisan test'
            }
        }
    }
    // Telegram Notification
    post{
            success{
                sh '''
                sh 1-success-deploy.sh;\
                '''
            }
            failure{
                sh '''
                sh 2-fail-deploy.sh;\
                '''
            }
    }

}
pipeline {
    agent any // window agent, Jenkins-laravel (other machine)
    
    stages {
        stage('Fetch from Github'){ //build steps
            steps {
                echo 'Fetching for Github'
                git branch: 'TP02', url: 'https://github.com/CHAB-Sreylen/Dev_ops.git'
            }
        }
        stage('Build using Tools'){
            steps{
                echo'Compiling Code ...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test app'){
            steps{
                echo 'Testing unit tests...'
                echo 'Testing feature...'
                sh 'php artisan test'
            }
        }
    }
    post {
        success {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1607234015\", \"text\": \"[SUCCESS] Ukata api build success!\", \"disable_notification\": false}\' https://api.telegram.org/bot6631869120:AAHaUSsakEu_xiB76WTZJPxSWvJXNo_ZjRs/sendMessage'
        }
        failure {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1607234015\", \"text\": \"[FAILED] Ukata api build failed!\", \"disable_notification\": false}\' https://api.telegram.org/bot6631869120:AAHaUSsakEu_xiB76WTZJPxSWvJXNo_ZjRs/sendMessage'
        }
    }

}
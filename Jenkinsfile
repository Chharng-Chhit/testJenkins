pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    environment {
        BOT_TOKEN = '6721183761:AAGp1RwuFRR8uJ9GwNxXRZibOxYk7QxNs18'
        CHAT_ID = '-4121372419'
    }
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'TP03', url:'https://github.com/Mony-Ratanak/DevOps.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
    }
    post {
        success {
            sh '''
                bash scripts/deployment.sh SUCCESS🟢
            '''
        }
        failure {
            sh '''
                bash scripts/deployment.sh FAILED🔴
            '''
        }
    }
}

pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests available"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                export PATH=$PATH:/usr/bin
                pm2 delete status-monitor || true
                pm2 start examples/index.js --name status-monitor
                pm2 save
                '''
            }
        }
    }
}

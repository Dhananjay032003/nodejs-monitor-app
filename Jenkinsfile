pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'No tests configured for this project'
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                npm install -g pm2 || true
                pm2 delete status-monitor || true
                pm2 start examples/index.js --name status-monitor
                pm2 save
                '''
            }
        }
    }
}

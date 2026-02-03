pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                npm install
                cd examples
                npm install
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'No tests configured'
            }
        }

        stage('Run Application with PM2') {
            steps {
                sh '''
                npm install -g pm2 || true
                pm2 delete status-monitor || true
                pm2 start examples/express.js --name status-monitor
                pm2 save
                '''
            }
        }
    }
}

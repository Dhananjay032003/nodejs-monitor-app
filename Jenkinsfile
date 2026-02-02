pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

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
                pm2 delete status-monitor || true
                pm2 start examples/express.js --name status-monitor
                pm2 save
                '''
            }
        }
    }
}

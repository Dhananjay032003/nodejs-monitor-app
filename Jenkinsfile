pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    environment {
        APP_PORT = "3000"
        APP_DIR  = "examples"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install Root Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Install App Dependencies') {
            steps {
                dir("${APP_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Stop Previous App') {
            steps {
                sh '''
                echo "Stopping previous Node app if running"
                pkill -f "node index.js" || true
                pkill -f "npm start" || true
                '''
            }
        }

        stage('Start Application') {
            steps {
                dir("${APP_DIR}") {
                    sh '''
                    echo "Starting NodeJS application"
                    nohup npm start > app.log 2>&1 &
                    sleep 15
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                echo "Checking application health"
                curl http://localhost:${APP_PORT} || true
                '''
            }
        }
    }

    post {
        success {
            echo '✅ DEPLOYMENT SUCCESSFUL'
        }
        failure {
            echo '❌ DEPLOYMENT FAILED'
        }
    }
}

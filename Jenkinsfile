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
                sh '''
                echo "Installing root dependencies"
                npm install
                '''
            }
        }

        stage('Install App Dependencies') {
            steps {
                dir("${APP_DIR}") {
                    sh '''
                    echo "Installing app dependencies"
                    npm install
                    '''
                }
            }
        }

        stage('Stop Previous App') {
            steps {
                sh '''
                echo "Stopping any running app on port ${APP_PORT}"
                fuser -k ${APP_PORT}/tcp || true
                '''
            }
        }

        stage('Start Application') {
            steps {
                dir("${APP_DIR}") {
                    sh '''
                    echo "Starting application"
                    nohup npm start > app.log 2>&1 &
                    sleep 10
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                echo "Verifying app deployment"
                curl -f http://localhost:${APP_PORT}
                '''
            }
        }
    }

    post {
        success {
            echo '🎉 DEPLOYMENT SUCCESSFUL — APP IS LIVE'
        }
        failure {
            echo '❌ DEPLOYMENT FAILED — CHECK LOGS'
        }
    }
}

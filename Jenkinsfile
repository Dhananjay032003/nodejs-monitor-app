pipeline {
    agent any

    environment {
        APP_PORT = "3000"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
                echo 'Workspace cleaned'
            }
        }

        stage('Checkout Code') {
            steps {
                echo 'Cloning repository'
                git branch: 'main',
                    url: 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install NodeJS & npm') {
            steps {
                sh '''
                if ! command -v node >/dev/null 2>&1; then
                  curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
                  sudo apt-get install -y nodejs
                fi

                node -v
                npm -v
                '''
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

        stage('Install Example App Dependencies') {
            steps {
                dir('examples') {
                    sh '''
                    echo "Installing example dependencies"
                    npm install
                    '''
                }
            }
        }

        stage('Start Example App') {
            steps {
                dir('examples') {
                    sh '''
                    echo "Starting example app on port 3000"
                    nohup npm start > app.log 2>&1 &
                    sleep 8
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                echo "Checking if app is running on port 3000"
                ss -tulnp | grep 300

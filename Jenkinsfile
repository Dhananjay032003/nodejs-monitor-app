pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning GitHub repository'
                git branch: 'main',
                    url: 'https://github.com/Dhananjay032003/nodejs-monitor-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                echo "Installing root dependencies"
                npm install

                echo "Installing example dependencies"
                cd examples
                npm install
                '''
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
                echo "Running NodeJS monitoring application"
                cd examples
                node index.js
                '''
            }
        }
    }

    post {
        success {
            echo '✅ BUILD & DEPLOYMENT SUCCESSFUL'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}

pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning repository'
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

        stage('Install Example App Dependencies') {
            steps {
                sh '''
                echo "Installing example app dependencies"
                cd examples
                npm install
                '''
            }
        }

        stage('Validate Project Structure') {
            steps {
                sh '''
                echo "Validating project structure"
                test -d examples
                test -f examples/package.json
                echo "Validation successful"
                '''
            }
        }

        stage('Run Example App (Non-blocking)') {
            steps {
                sh '''
                echo "Starting example app"
                cd examples
                nohup npm start > app.log 2>&1 &
                sleep 5
                '''
            }
        }
    }

    post {
        success {
            echo '✅ PIPELINE COMPLETED SUCCESSFULLY'
        }
        failure {
            echo '❌ PIPELINE FAILED'
        }
    }
}

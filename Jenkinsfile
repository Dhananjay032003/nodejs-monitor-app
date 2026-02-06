pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

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

        stage('Validate Application') {
            steps {
                sh '''
                echo "Validating NodeJS project structure"
                test -f examples/index.js
                echo "Validation successful"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ BUILD SUCCESSFUL'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}

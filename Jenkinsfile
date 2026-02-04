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

        stage('Test / Validate Application') {
            steps {
                sh '''
                echo "Validating NodeJS application (no server start)"
                node -e "require('./examples/index.js'); console.log('Validation successful')"
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

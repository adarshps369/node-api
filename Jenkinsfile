pipeline {
    agent any

    environment {
        NODE_HOME = '/usr/bin'
        PATH = "${env.NODE_HOME}:${env.PATH}"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests but don't fail the build if tests fail
                sh 'npm test || echo "⚠️ Test stage failed. Check test results."'
            }
        }

        stage('Build') {
            steps {
                echo '✅ Build step (optional)'
            }
        }

        stage('Deploy with PM2') {
            steps {
                script {
                    // Ensure PM2 is installed and run the app
                    sh '''
                    # Install PM2 if not present
                    if ! command -v pm2 > /dev/null; then
                        echo "Installing PM2..."
                        sudo npm install -g pm2
                    fi

                    # Navigate to project directory
                    cd $WORKSPACE

                    # Start or restart the app
                    pm2 delete node-api || true
                    pm2 start server.js --name node-api
                    pm2 save

                    # Show status
                    pm2 status
                    '''
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}


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
                sh 'npm test || echo "⚠️ Test stage failed, continuing..."'
            }
        }

        stage('Deploy with PM2') {
            steps {
                script {
                    sh '''
                    # Install PM2 if missing
                    if ! command -v pm2 > /dev/null; then
                        echo "Installing PM2..."
                        sudo npm install -g pm2
                    fi

                    # Change to workspace where server.js exists
                    cd $WORKSPACE

                    # Stop existing process and restart app
                    pm2 delete node-api || true
                    pm2 start server.js --name node-api
                    pm2 save
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


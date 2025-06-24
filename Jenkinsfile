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
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Build step (optional)'
            }
        }

        stage('Deploy with PM2') {
            steps {
                script {
                    sh '''
                    pm2 delete node-api || true
                    pm2 start server.js --name node-api
                    pm2 save
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


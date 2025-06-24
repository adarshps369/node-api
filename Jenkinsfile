pipeline {
    agent any

    environment {
        NODE_HOME = '/usr/bin'
        PATH = "${env.NODE_HOME}:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/scotch-io/node-api.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "Tests failed but continuing..."'
            }
        }

        stage('Build (Simulated)') {
            steps {
                echo 'Simulating build step...'
                sh 'mkdir -p build && cp -r * build/'
            }
        }

        stage('Deploy (Simulated)') {
            steps {
                echo 'Simulated deploy to /tmp/node-api-deploy'
                sh 'mkdir -p /tmp/node-api-deploy && cp -r build/* /tmp/node-api-deploy'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}


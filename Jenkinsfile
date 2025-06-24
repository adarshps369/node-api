pipeline {
    agent any

    environment {
        NODE_HOME = '/usr/bin'
        PATH = "${env.NODE_HOME}:${env.PATH}"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/adarshps369/node-api.git'
            }
        }

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
                echo 'Simulating build process...'
                sh 'mkdir -p build && cp -r * build/'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Simulated deploy to /tmp/node-api-deploy'
                sh 'mkdir -p /tmp/node-api-deploy && cp -r build/* /tmp/node-api-deploy'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}


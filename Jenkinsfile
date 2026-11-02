
pipeline {
    agent any

    environment {
        PATH = "${WORKSPACE}/.node/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Install Node.js 22') {
            steps {
                sh '''
                    mkdir -p "$WORKSPACE/.node"
                    curl -fsSL https://nodejs.org/dist/v22.14.0/node-v22.14.0-linux-x64.tar.xz -o node.tar.xz
                    tar -xJf node.tar.xz -C "$WORKSPACE/.node" --strip-components=1
                    node --version
                    npm --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'mkdir -p deployed-app'
                sh 'cp -r dist/. deployed-app/'
                echo 'Application deployed successfully!'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Completed Successfully!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}
s

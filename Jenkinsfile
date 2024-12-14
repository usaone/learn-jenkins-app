pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u node'
                    reuseNode true
                }
            }

            steps {
                cleanWs()
                sh '''
                    ls -la
                    mkdir -p .npm_cache
                    npm config set cache .npm_cache
                    npm config set prefix .npm_cache
                    npm config set global true
                    export PATH=$PATH:./.npm_global/bin
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
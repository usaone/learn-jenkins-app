pipeline {
    agent any

    stages {
        stage('Build') {
            options {
                timeout(time: 15, unit: 'MINUTES')
            }
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '--memory=4g --memory-swap=4g'
                }
            }

            steps {
                cleanWs()
                sh '''
                    mkdir -p .npm_cache
                    npm config set cache .npm_cache
                    npm config set prefix .npm_global
                    export PATH=$PATH:./.npm_global/bin
                    npm --version
                    node --version
                    npm install --loglevel verbose
                    npm run build
                    ls -la
                '''
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
          
            steps {
                sh '''
                      ls -la
                      node --version
                      npm --version
                      npm ci
                      npm run build
                      ls -la 
                '''
            }
        }
        stage('E2E Tests') {

            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.34.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                      npm install -g serve
                      node_modules/.bin/serve -s build
                      npx playwright test
                    '''
            }
        }
    }
}
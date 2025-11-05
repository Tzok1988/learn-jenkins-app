pipeline {
    agent any
    environment {
        NETLIFY_SITE_ID = '88b2d35d-78f7-4678-a3f8-51455e0666e0' 
        NETLIFY_AUTH_TOKEN = credentials('netlify-auth-token')
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-bullseye'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    set -e
                    npm ci
                    npm run build
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-bullseye'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f ./build/index.html
                    npm test
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-bullseye'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    set -e
                    npx install netlify-cli
                    npx netlify --version
                    echo "Deploying to production Netlify site ID: $NETLIFY_SITE_ID"
                    npx netlify status
                    npx netlify deploy --dir=./build --prod
                '''
            }
        }
    }
}
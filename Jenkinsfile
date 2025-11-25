pipeline {
    agent any

    stages {
        stage('w/o docker ') {
            steps {
                echo "Job without using docker "
                sh '''
                pwd
                touch container-no.txt
                ls -altr
                '''
            }
        }
        
        stage('with docker ') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            
            steps {
                echo "Job wehn using docker "
                sh '''
                    npm --version
                    pwd
                    touch container-yes.txt
                    ls -altr
                '''
            }
        }
    }
}

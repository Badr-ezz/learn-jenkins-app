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
                pwd
                node --version
                npm --version
                npm ci 
                npm run build 
                ls -la
                '''                
            }

        }
        stage('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }    
    }

    post {
        always {
            sh 'echo "test Report " '
            junit 'test-results/junit.xml' // show the test report  
        }
    }
}

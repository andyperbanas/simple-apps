pipeline {
    agent {
        node {
            label 'devops-andi'
        }
    }

    stages {
        stage('Build Apps') {
            steps {
                sh '''
                cd apps
                npm install
                '''
            }
        }
        
        stage('Copy env') {
            steps {
                sh '''
                sudo cp /root/simple-apps/apps/.env apps/
                '''
            }
        }

        stage('Test Apps') {
            steps {
                sh '''
                cd apps
                npm test
                npm run test:coverage
                '''
            }
        }

        stage('Scanning Code') {
            steps {
                sh '''
                cd apps
                sonar-scanner   -Dsonar.projectKey=Simple-Apps   -Dsonar.sources=.   -Dsonar.host.url=http://172.23.2.2:9000   -Dsonar.login=sqp_91d46325d7129b37b6d30e6b5c97392733c2b91a
                '''
            }
        }

        stage('Dockerized') {
            steps {
                sh '''
                docker compose build
                '''
            }
        }

        stage('Deploy Apps') {
            steps {
                echo "Process Deploy Apps"
            }
        }

        stage('Publish Image') {
            steps {
                echo "Process Publish Image"
            }
        }
    }
}

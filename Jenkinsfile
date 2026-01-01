pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm  
            }
        }

        stage('Build App') {
            steps {
                sh './scripts/build.sh'  
            }
        }

        stage('Test App') {
            steps {
                sh './scripts/test.sh'  
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myfirstapp .'
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_creds_id') {
                        sh 'docker tag myfirstapp sagitzhanov/myfirstapp:latest'
                        sh 'docker push sagitzhanov/myfirstapp:latest'
                    }
                }
            }
        }
    }
}

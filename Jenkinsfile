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
                withCredentials([usernamePassword(credentialsId: 'docker_hub_creds_id', 
                                         usernameVariable: 'DOCKER_USER', 
                                         passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        docker login -u $DOCKER_USER -p $DOCKER_PASS
                        docker tag myfirstapp $DOCKER_USER/myfirstapp:latest
                        docker push $DOCKER_USER/myfirstapp:latest
                    '''
                }
            }
        }
    }
}

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
    }
}

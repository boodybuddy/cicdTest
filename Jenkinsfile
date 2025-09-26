pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker') {
            steps {
                sh 'docker build -t 47.83.3.100/jenkins/cicdtest:latest .'
            }
        }
        stage('Login Harbor') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'harbor-robot',
                                                 usernameVariable: 'HARBOR_USER',
                                                 passwordVariable: 'HARBOR_PASS')]) {
                    sh 'echo $HARBOR_PASS | docker login 47.83.3.100 -u $HARBOR_USER --password-stdin'
                }
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push 47.83.3.100/jenkins/cicdtest:latest'
            }
        }
    }
}

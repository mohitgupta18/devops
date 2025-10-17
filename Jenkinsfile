pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('366d7429-4efd-4644-8f72-f6ce654a3fd0')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/mohitgupta18/devops.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t mohitg432/image:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push mohitg432/image:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

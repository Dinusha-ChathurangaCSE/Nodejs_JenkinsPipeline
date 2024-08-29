pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'master', url: 'https://github.com/Dinusha-ChathurangaCSE/Nodejs_JenkinsPipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                sh 'docker build -t dinusha2001/nodeapp-cuban:${BUILD_NUMBER} .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u dinusha2001 -p ${dockerhubpwd}'
                    }
                }
            }
        
        stage('Push Image') {
            steps {
                sh 'docker push dinusha2001/nodeapp-cuban:${BUILD_NUMBER}'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}

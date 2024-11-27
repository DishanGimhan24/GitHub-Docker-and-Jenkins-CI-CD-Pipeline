pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/HGSChandeepa/test-node'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t dishangimhan/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                
                withCredentials([string(credentialsId: 'test-dockerhubpassword1', variable: 'test-dockerhubpassword1')]) {
                    
                        bat "docker login -u dishangimhan -p %test-dockerhubpassword1%"
                  
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push dishangimhan/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}

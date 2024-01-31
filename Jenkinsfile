pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shreegs123/Guvi_Interview_Task.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t task-img .'
                sh 'docker tag task-img $DOCKER_IMAGE'
                
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 80:80 --name task-cont task-img'
            }
        }
            
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
                sh 'docker push $DOCKER_IMAGE'
            }
        }
        
        }
    }
    
}

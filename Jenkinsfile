pipeline {
    agent { label 'jenkins-agent' }
    environment {
        REGISTRY = '192.168.20.90:5000'
        IMAGE1    = 'todo-app'
        IMAGE2    = 'todo-backend'
    }
    stages {
        stage('Build image') {
            steps {
                sh 'docker build -f app/Dockerfile -t $REGISTRY/$IMAGE1:$BUILD_NUMBER -t $REGISTRY/$IMAGE1:latest app/'
                sh 'docker build -f app/backend/Dockerfile -t $REGISTRY/$IMAGE2:$BUILD_NUMBER -t $REGISTRY/$IMAGE2:latest app/backend/'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push $REGISTRY/$IMAGE1:$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$IMAGE1:latest'
                sh 'docker push $REGISTRY/$IMAGE2:$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$IMAGE2:latest'
            }
        }
    }
}

pipeline {
    agent { label 'jenkins-agent' }
    environment {
        REGISTRY = '192.168.20.90:5000'
        IMAGE    = 'todo-app'
    }
    stages {
        stage('Build image') {
            steps {
                sh 'docker build -f app/Dockerfile -t $REGISTRY/$IMAGE:$BUILD_NUMBER -t $REGISTRY/$IMAGE:latest app/'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push $REGISTRY/$IMAGE:$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$IMAGE:latest'
            }
        }
    }
}

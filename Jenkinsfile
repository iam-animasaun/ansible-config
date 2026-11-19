pipeline {
    agent { label 'jenkins-agent' }
    environment {
        REGISTRY = '192.168.20.90:5000'
        IMAGE    = 'todo-app'
    }
    stages {
        stage('SonarQube analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonar-scanner'
                    withSonarQubeEnv('sonarcloud') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.organization=iam-animasaun -Dsonar.projectKey=iam-animasaun_ansible-config -Dsonar.sources=. -Dsonar.host.url=\$SONAR_HOST_URL -Dsonar.token=\$SONAR_AUTH_TOKEN"
                    }
                }
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -f app/ -t $REGISTRY/$IMAGE:$BUILD_NUMBER -t $REGISTRY/$IMAGE:latest .'
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

pipeline {
    agent { label 'jenkins-agent' }
    stages {
        stage('Run playbook') {
            steps {
                sh 'ansible-playbook -i inventory.ini site.yml'
            }
        }
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
    }
}

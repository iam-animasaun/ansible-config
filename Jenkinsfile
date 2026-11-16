pipeline {
    agent { label 'jenkins-agent' }
    stages {
        stage('Run playbook') {
            steps {
                sh 'ansible-playbook -i inventory.ini site.yml'
            }
        }
    }
}

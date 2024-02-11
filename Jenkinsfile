pipeline {
    agent any
    
    stages {
        stage('Print Hello') {
            steps {
                script {
                    echo 'Pulling... ' + env.GIT_BRANCH
                }
            }
        }
        stage('Run ansible playbook') {
            steps {
                ansiblePlaybook(
                    playbook: 'playbook.yml',
                    inventory: 'inventory.hosts')
            }
        }
    }
}

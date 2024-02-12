pipeline {
    agent any
    
    environment {
        BRANCH_NAME = "${env.GIT_BRANCH.split('/')[-1]}"
    }
    
    stages {
        stage('Run ansible playbook') {
            steps {
                script {
                    echo 'Pulling... ' + env.GIT_BRANCH
                    ansiblePlaybook(
                        playbook: "${BRANCH_NAME}.yml",
                        inventory: 'inventory.hosts',
                        installation: 'Ansible')
                }
            }
        }
        
        stage('Test ansible playbook') {
            steps {
                script {
                    ansiblePlaybook(
                        playbook: "tests/${BRANCH_NAME}.yml",
                        inventory: 'inventory.hosts',
                        installation: 'Ansible')
                }
            }
        }
    }
}

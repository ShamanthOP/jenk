pipeline {
    agent any
    
    stages {
        stage('Run ansible playbook') {
            steps {
                script {
                    echo 'Pulling... ' + env.GIT_BRANCH
                    def branchName = env.GIT_BRANCH
                    def playbookName = branchName.split('/')[-1]
                    ansiblePlaybook(
                        playbook: "${playbookName}.yml",
                        inventory: 'inventory.hosts',
                        installation: 'Ansible')
                }
            }
        }
    }
}

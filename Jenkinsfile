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

                    def ansibleInventoryPath = sh(script: 'which ansible-inventory', returnStdout: true).trim()
                    def inventoryOutput = sh(script: '${ansibleInventoryPath} -i inventory.hosts --list', returnStdout: true).trim()
                    def json = readJSON text: inventoryOutput
                    def groups = json.keySet().findAll { it != "_meta" && it != "all" }
                    echo "Groups: ${groups}"

                    def random = new Random()
                    def randomGroup = groups[random.nextInt(groups.size())]
                    
                    echo "Randomly selected group: ${randomGroup}"

                    // ansiblePlaybook(
                    //     playbook: "${BRANCH_NAME}.yml",
                    //     inventory: 'inventory.hosts',
                    //     installation: 'Ansible')
                }
            }
        }
        
        // stage('Test ansible playbook') {
        //     steps {
        //         script {
        //             ansiblePlaybook(
        //                 playbook: "tests/${BRANCH_NAME}.yml",
        //                 inventory: 'inventory.hosts',
        //                 installation: 'Ansible')
        //         }
        //     }
        // }
    }
}

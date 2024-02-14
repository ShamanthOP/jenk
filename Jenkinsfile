def randomGroup

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

                    def queueItems = Jenkins.instance.getQueue().getItems()
                    queueItems.each { item ->
                        println "Item: ${item}"
                    }

                    sleep time: 30, unit: 'SECONDS'

                    def inventoryOutput = sh(script: '/usr/local/bin/ansible-inventory -i inventory.hosts --list', returnStdout: true).trim()
                    def json = readJSON text: inventoryOutput
                    def groups = json.keySet().findAll { it != "_meta" && it != "all" }
                    echo "Groups : ${groups}!"

                    def random = new Random()
                    randomGroup = groups[random.nextInt(groups.size())]
                    
                    echo "Randomly selected group: ${randomGroup}"

                    ansiblePlaybook(
                        playbook: "${BRANCH_NAME}.yml",
                        inventory: 'inventory.hosts',
                        installation: 'Ansible',
                        limit: randomGroup)
                }
            }
        }
        
        stage('Test ansible playbook') {
            steps {
                script {
                    ansiblePlaybook(
                        playbook: "tests/${BRANCH_NAME}.yml",
                        inventory: 'inventory.hosts',
                        installation: 'Ansible',
                        limit: randomGroup)
                }
            }
        }
    }
}

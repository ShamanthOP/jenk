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
        stage('Sleep') {
            steps {
                script {
                    sleep time: 16, unit: 'SECONDS'
                }
            }
        }
    }
}

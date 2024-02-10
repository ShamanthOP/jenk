pipeline {
    agent any
    
    stages {
        stage('Print Hello') {
            steps {
                script {
                    echo 'Hello, World!'
                }
            }
        }
        stage('Sleep') {
            steps {
                script {
                    sleep time: 5, unit: 'SECONDS'
                }
            }
        }
    }
}

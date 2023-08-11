pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sshagent(credentials: ['instance-1']) {
                        def remoteDeployScript = sh(script: 'cat deploy.sh', returnStdout: true).trim()
                        sshCommand remote: 'mohamadzaelani09@35.224.120.106', command: remoteDeployScript
                    }
                }
            }
        }
    }
}

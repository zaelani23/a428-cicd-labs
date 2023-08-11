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
                        sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@35.224.120.106 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/deliver.sh'
                        sleep 1m
                        sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@35.224.120.106 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/kill.sh'
                    }
                }
            }
        }
    }
}

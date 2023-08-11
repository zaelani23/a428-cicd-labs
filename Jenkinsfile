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
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@18.140.5.87 sh /home/mohamadzaelani09/a433-cicd-labs/jenkins/scripts/deliver.sh'
                        sleep 1m
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@18.140.5.87 sh /home/mohamadzaelani09/a433-cicd-labs/jenkins/scripts/kill.sh'
                    }
                }
            }
        }
    }
}

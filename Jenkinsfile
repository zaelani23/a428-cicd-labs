pipeline {
    agent {
        docker {
            image 'node:16' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
         stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval'){
            steps{
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sshagent(credentials: ['instance-1']) {
                        sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@34.28.94.220 cd /home/mohamadzaelani09/a428-cicd-labs/ && git pull origin react-app'
                        sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@34.28.94.220 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/deliver.sh'
                        sleep(time: 1, unit: 'MINUTES')
                        sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@34.28.94.220 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/kill.sh'
                    }
                }
            }
        }
    }
}

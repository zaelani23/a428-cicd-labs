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
                    sh '''
                        sudo apt-get update
                        sudo apt-get install -y openssh-client
                    '''
                    sh 'ssh-agent bash -c "ssh-add /var/jenkins_home/.ssh/id_rsa; ssh -o StrictHostKeyChecking=no mohamadzaelani09@34.28.94.220 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/deliver.sh"'
                    sleep(time: 1, unit: 'MINUTES')
                    sh 'ssh -o StrictHostKeyChecking=no mohamadzaelani09@34.28.94.220 sh /home/mohamadzaelani09/a428-cicd-labs/jenkins/scripts/kill.sh'
                }
            }
        }
    }
}

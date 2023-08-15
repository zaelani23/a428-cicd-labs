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
                    def remoteCommands = """
                        cd /home/ec2-user/a428-cicd-labs/
                        git pull origin react-app
                        npm start &
                    """
                    sshagent(credentials: ['ec2-user']) {
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@ec2-54-166-250-178.compute-1.amazonaws.com '''${remoteCommands}'''"
                        sleep(time: 1, unit: 'MINUTES')
                        sh 'ssh -o StrictHostKeyChecking=no ec2-user@ec2-54-166-250-178.compute-1.amazonaws.com sh /home/ec2-user/a428-cicd-labs/jenkins/scripts/kill.sh'
                    }
                }
            }
        }
    }
}

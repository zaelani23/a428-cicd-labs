pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
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
                //sh './jenkins/scripts/kill.sh'
            }
        }
         stage('Deploy') {
            steps {
                sshagent(['mfajrizulfa']){
                    sh '''
                    ssh -i "deploy.pem" ubuntu@ec2-13-250-64-22.ap-southeast-1.compute.amazonaws.com'''
                }
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: 'MINUTES')
            }
        }
    }
}
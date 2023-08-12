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
            }
        }
    	stage('Checkout') {
        	steps {
            	checkout scm
        	}
    	}
         stage('Deploy') {
            steps {
                script {
  	              sshagent(credentials: ['ubuntu']) {
                    	sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.250.64.22 sh /home/ubuntu/a428-cicd-labs/jenkins/scripts/deliver.sh'
                    	sleep(time: 1, unit: 'MINUTES')
                    	sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.250.64.22 sh /home/ubuntu/a428-cicd-labs/jenkins/scripts/kill.sh'
                	}
            	}
            }
        }
    }
}
/*sshagent(['mfajrizulfa']){
                //    sh '''ssh -o StrictHostChecking=no ubuntu@ec2-13-250-64-22.ap-southeast-1.compute.amazonaws.com'''
                //}
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: 'MINUTES')
                script {
  	              sshagent(credentials: ['ubuntu']) {
                    	sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.250.64.22 sh /home/ubuntu/a428-cicd-labs/jenkins/scripts/deliver.sh'
                    	sleep(time: 1, unit: 'MINUTES')
                    	sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.250.64.22 sh /home/ubuntu/a428-cicd-labs/jenkins/scripts/kill.sh'
                	}
            	}
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh'
                */
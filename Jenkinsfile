node {

    env.PATH = "${tool 'NodeJS'}/bin:${env.PATH}"

    docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
        stage('Build') {
            sh 'cd . && npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}

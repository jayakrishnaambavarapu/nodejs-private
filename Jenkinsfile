pipeline {
    agent any

    stages {
        stage('git') {
            steps {
                checkout scm
            }
        }
        stage('build') {
            steps {
            sh 'docker login -u jayak8309101680 -p Ak18@&deb
            sh 'docker build -t sample1 .'
            sh 'docker tag sample1 jayak8309101680/frontend:v5'
            
            }
        }
        stage('deploy') {
            steps {
                sshagent(credentials : ['terraform']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.84.157.118 docker run -itd -p 8082:8081 jayak8309101680/frontend:v5'
                }
            }
        }
    }
}

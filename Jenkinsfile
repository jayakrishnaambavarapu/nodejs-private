pipeline {
    agent any
    environment {
        jayakrsna=credentials('docker-credentials')
    }

    stages {
        
        stage('git') {
            steps {
                checkout scm
        }
        
        stage('build') {
            steps {
          
            sh 'docker build -t sample1 .'
            sh 'docker tag sample1 jayak8309101680/frontend:v5'
            
            sh 'echo $jayakrsna_PSW | docker login -u $jayakrsna_USR --password-stdin'
            sh 'docker push jayak8309101680/frontend:v5'
            
            }
        }
        stage('deploy to app host') {
            steps {
                sshagent(credentials : ['terraform']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@34.239.106.195 docker run -itd -p 8082:8081 jayak8309101680/frontend:v5'
                }
            }
        }
    }
}

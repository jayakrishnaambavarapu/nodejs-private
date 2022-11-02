pipeline {
    agent any

    stages {
        
        stage('build') {
            steps {
          
            sh 'docker build -t sample1 .'
            sh 'docker tag sample1 jayak8309101680/frontend:v5'
            
            sh 'docker login -u jayak8309101680 -p "Ak18@&deb"'
            sh 'docker push jayak8309101680/frontend:v5'
            
            }
        }
        stage('deploy') {
            steps {
                sshagent(credentials : ['terraform']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@34.239.106.195 docker run -itd -p 8082:8081 jayak8309101680/frontend:v5'
                }
            }
        }
    }
}

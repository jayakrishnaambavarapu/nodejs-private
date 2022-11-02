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
                sh 'docker build -t nodejs-sample-app .'
                sh 'docker tag nodejs-sample-app 587173959192.dkr.ecr.us-east-1.amazonaws.com/sample:v1'
               
            
                script {
                    docker.withRegistry("https://587173959192.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:aws-credentials") { 
                        docker.image("587173959192.dkr.ecr.us-east-1.amazonaws.com/sample:v1").push()
                    }
                }
            
            
            }
        }
        stage('deploy to app host') {
            steps {
                sshagent(credentials : ['app']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@10.0.4.169 docker run -itd -p 8080:8081 587173959192.dkr.ecr.us-east-1.amazonaws.com/sample'
                }
            }
        }
    }
}

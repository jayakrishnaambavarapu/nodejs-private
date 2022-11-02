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
                sh 'docker tag nodejs-sample-app public.ecr.aws/u2e2e7i0/nodejs-app:v1'
                sh 'docker push public.ecr.aws/u2e2e7i0/nodejs-app:v1'
            
                script {
                    docker.withRegistry("https://public.ecr.aws/u2e2e7i0", "ecr:us-east-1:aws-credentials") { 
                        docker.image("public.ecr.aws/u2e2e7i0/nodejs-app:v1").push()
                    }
                }
            
            
            }
        }
        stage('deploy to app host') {
            steps {
                sshagent(credentials : ['app']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@10.0.4.169 docker run -itd -p 8080:8081 public.ecr.aws/u2e2e7i0/nodejs-app:v1'
                }
            }
        }
    }
}

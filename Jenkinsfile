pipeline{
    agent any
    environment {
        Docker_Image_Name = 'myimage'
        Docker_Tag = 'v2'
    }
    options { timestamps()
    buildDiscarder(logRotator(numToKeepStr: '10'))
    disableConcurrentBuilds()
    }
    stages{
        
        stage ('Pre-Checks'){
        
            parallel {
              stage ('Docker-Verify') {
                  steps {
                sh "docker --version"
                  }
                  }
              stage ('Git-Verify') {
                  steps {
                sh "git --version"
                  }
                  }
            }
         
        }
    
        stage ('Docker-Build') {
            when {
            expression {  
                  return env.GIT_BRANCH == "origin/main" 
                   }
               }
        
            steps {
                sh 'aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 531726073249.dkr.ecr.ap-south-1.amazonaws.com'
                sh "sudo docker build -t my-jenkins-project:${env.BUILD_NUMBER} ."
                sh "sudo docker tag my-jenkins-project:${env.BUILD_NUMBER} 531726073249.dkr.ecr.ap-south-1.amazonaws.com/my-jenkins-project:${env.BUILD_NUMBER}"
                sh "sudo docker push 531726073249.dkr.ecr.ap-south-1.amazonaws.com/my-jenkins-project:${env.BUILD_NUMBER}"
            }
        }
        stage ('Docker-Image-verify') {
            steps {
              sh "sudo docker images"
              sh "sudo docker ps"
            }
        }
        stage ('Docker-CleanUp') {
            steps {
              sh 'sudo docker rm -f \$(sudo docker ps -a -q) 2> /dev/null || true' 
            }
        }
        stage ('Docker-Deploy') {
            input {
                message "deploy ?"
            }
            steps {
              sh "sudo docker run -itd -p 80:80 531726073249.dkr.ecr.ap-south-1.amazonaws.com/my-jenkins-project:${env.BUILD_NUMBER}"
              sh "sudo docker ps"
            }
        }
         stage ('Docker-Images-CleanUp') {
            steps {
              sh 'sudo docker image prune -af' 
            }
        }
    }
    post {
    always {
    sh 'sudo docker images'
    }
    aborted {
    sh 'sudo docker ps'
    }
    }
}

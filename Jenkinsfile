pipeline{
    agent any
    stages{
        stage ('build') {
            steps {
              sh "docker --version"  
            }
        }
        
        stage ('Git-verify') {
            steps {
              sh "git --version"  
            }
        }
        stage ('Docker-Build') {
            steps {
              sh "sudo docker build -t myimage:v1 ."  
            }
        }
        stage ('Docker-Image-verify') {
            steps {
              sh "sudo docker images"
              sh "sudo docker ps"
            }
        }

    }
}

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
              sh "sudo docker build -t myimage:v1"  
            }
        }

    }
}

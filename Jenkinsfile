pipeline{
    agent any
    environment {
        Docker_Image_Name = 'myimage'
        Docker_Tag = 'v2'
    }
    stages{
        stage ('docker-verify') {
            steps {
                retry(3) {
              sh "doker --version"  
                }
             }
        }
        
        stage ('Git-verify') {
            steps {
              sh "git --version"  
            }
        }
        stage ('Docker-Build') {
            steps {
                sh "sudo docker build -t ${Docker_Image_Name}:${env.BUILD_NUMBER} ."  
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

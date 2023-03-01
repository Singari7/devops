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
    }
}
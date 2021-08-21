pipeline{
    agent any
    tools {
      maven 'maven-3.8.2'
    }
    environment {
      DOCKER_TAG = getVersion()
    }
 
    stages{
        stage('SCM'){
            steps{
                git branch: 'main', credentialsId: 'git-pass', url: 'https://github.com/fculibao/dockeransiblejenkins.git'
            }    
        }
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('Docker Build'){
            steps{
                sh "docker build . -t fculibao/nodeapp:0.0.1 ."
            }
        }
    }
    
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}  
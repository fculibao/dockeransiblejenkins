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
                sh "docker build . -t fculibao/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-access-pwd', variable: 'dockerHubPwd')]) {
                sh "docker login -u fculibao -p ${dockerHubPwd}"
                }
                sh "docker push fculibao/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('Docker Deploy'){
            steps{
              ansiblePlaybook credentialsId: 'ec2-user', disableHostKeyChecking: true, extras: "-e DOCKER_TAG=${DOCKER_TAG}", installation: 'ansible', inventory: 'dev.inv', playbook: 'deploy-docker.yml'
            }
        }
    }
    
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}  
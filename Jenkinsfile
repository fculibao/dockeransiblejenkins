pipeline{
    agent any
    tools {
      maven 'maven-3.8.2'
    }
    environment {
      DOCKER_TAG = getVersion()
    }
    stages{
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('Docker Build'){
            steps{
                sh "docker build . -t fculibao/nodeapp:${DOCKER_TAG} "
            }
        }
    }
    
}
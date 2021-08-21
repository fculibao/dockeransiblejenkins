pipeline{
    agent any
    tools {
      maven 'maven-3.8.2'
    }
    stages{
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
    }
    
}
pipeline{
    agent any
    tools {
      maven 'maven-3.8.2'
    }
    stages{
        stage('SCM'){
            steps{
                git credentialsId: 'git-pass', 
                    url: 'https://github.com/fculibao/dockeransiblejenkins'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
    }
    
}
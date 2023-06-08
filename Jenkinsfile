pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                 git branch: 'main', url: 'https://github.com/prakash505/demoapp.git'    
              
                          
                }
            }
         stage('unit testing'){
            
            steps{
                bat 'mvn test'  
            }
         }
        stage('integration testing'){
            steps{
                bat 'mvn verify -DskipUnitTests'
            }
        }
        stage('maven build'){
            steps{
                bat 'mvn clean install'
            }
        } 
        stage('sonarqube analysis'){
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'jenkins-sonar-token') {
                    bat 'mvn clean package sonar:sonar'
                    
                }        
            }
        }
     
    } 
        stage('quality gates'){
            steps{
                waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonar-token'
            }
  }  
}    

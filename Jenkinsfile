pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                 script{
                 git branch: 'main', url: 'https://github.com/prakash505/demoapp.git'    
              
                          
                }
            }
        }
         stage('unit testing'){
            
            steps{
                 script{
                bat 'mvn test'  
            }
          }
         }
        stage('integration testing'){
            steps{
                 script{
                bat 'mvn verify -DskipUnitTests'
            }
          }
        }
        stage('maven build'){
            steps{
                 script{
                bat 'mvn clean install'
            }
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
                 script{
                waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonar-token'
            }
          } 
       }
        
    stage('upload war file to nexus'){
        steps{
             script{
            nexusArtifactUploader artifacts: 
                [
                    [
                        artifactId: 'springboot',
                        classifier: '', 
                        file: 'target/Uber.jar', 
                        type: 'jar']
                ],
                credentialsId: 'nexus3-auth', 
                groupId: 'com.example', 
                nexusUrl: 'localhost:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'demoapp-release',
                version: '1.0.0'
           }
        }
    }
  }
}
   



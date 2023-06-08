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
    stage('upload jar file to nexus'){
        steps{
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
   



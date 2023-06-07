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
     
    } 
   
}     

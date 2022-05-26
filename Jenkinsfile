pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/SriSuryaTej/js-e2e-express-server.git'
      }
    }
     
    stage('Build') {
      steps {
        sh 'npm install'
        
      }
    }  
    
            
    stage('Test') {
      steps {
        sh 'node test'
      }
    }
  }
}
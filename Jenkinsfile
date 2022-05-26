pipeline {
  agent {label 'node_js'}
    
    
  stages {
        
    stage('Git') {
      steps {
        git branch: 'declarative', url: 'https://github.com/SriSuryaTej/js-e2e-express-server.git'
      }
    }
     
    stage('Build') {
      steps {
        sh 'npm install'
        
      }
    }  

  }
}
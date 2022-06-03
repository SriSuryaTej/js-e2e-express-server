pipeline {
  agent {label 'NODE_JS'}
  tools {
      nodejs 'NODE_JS'
  }
  stages {
        
    stage('Git') {
      steps {
        git branch: 'declarative', url: 'https://github.com/SriSuryaTej/js-e2e-express-server.git'
      }
    }
    stage ('Artifactory configuration') {
      steps {
        rtNpmDeployer (
          id: "NPM_DEPLOYER",
          serverId: 'JFROG_OSS',
          repo: 'surya-maven-releases'
            )                
           }
        } 
    stage('Installing_Dependencies') {
      steps {
        sh 'npm install'
        
      }
    }  
    stage('Build'){
      steps{
        sh 'npm run build'
      }
    }
    stage('Server_Up'){
      steps{
        sh 'nohup npm start &'
      }
    }
    stage('packing ') {
      steps {
        sh 'npm run pack'
          }
        }
    stage('Test results') {
      steps {
        sh 'npm test'
          }
        }

    stage('Quality Check'){
      steps{
        sh 'npm install sonarqube-scanner --save-dev'
        sh 'npm run sonar'
      }
    }
    stage ('Exec npm publish') {
      steps {
        rtNpmPublish (
          tool: 'NODE_JS',
          deployerId: "NPM_DEPLOYER"
             )
            }
        }
    stage ('Publish build info') {
      steps {
        rtPublishBuildInfo (
          serverId: "JFROG_OSS"
             )
          }
     }
  }
}
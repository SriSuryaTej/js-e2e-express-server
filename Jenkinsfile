pipeline {
	    agent { label 'NODE_JS' }
	    triggers {
	        cron('0 * * * *')
	    }
	    stages {
	        stage('SourceCode') {
	            steps {
	                git branch: 'declarative', url: 'https://github.com/SriSuryaTej/js-e2e-express-server.git'
	            }
	        }
	        stage('Dependencies') {
	            steps {
	                sh 'npm install'
	            }
	        }
	        stage('Build') {
	            steps {
	                sh 'npm run build'
	            }
	        }
	        stage('Test results') {
	            steps {
	                sh 'npm test'
	            }
	        }
	        stage('Sonar Analysis') {
	            steps {
	                sh 'npm install sonarqube-scanner --save-dev'
	                sh 'npm run sonar'
	            }
	        }
	        stage ('Artifactory configuration') {
	            steps {
	                
	                rtNpmDeployer (
	                    id: "NPM_DEPLOYER",
	                    serverId: "JFROG_OSS",
	                    repo: "myecomm-npm-local"
	                )
	            }
	        }
	

	      
	

	        stage ('Exec npm publish') {
	            steps {
	                rtNpmPublish (
	                    tool: 'Node_JS',
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
	              

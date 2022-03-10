def VERSION = "1.0.0"
pipeline {
    agent any
  tools {
    maven 'maven3'
	}
	stages{
	    stage('Build') {
		  steps{
		      sh 'mvn clean package'
			  script {
                    VERSION = readMavenPom().getVersion()
                }
                echo("Build version: ${VERSION}") 
      }
      }
	    stage('sonarqube analysis') {
		     steps{
			      withSonarQubeEnv('sonarqube') {
				  sh "mvn sonar:sonar"
				  }
			}
		}
		stage("Quality Gate") {
		steps {
		//timeout(time:1, unit: 'SECONDS') {
		//waitForQualityGate abortPipeline: true
		//}
		        echo 'test'
		}
	  }
	  stage('upload war to nexus'){
          steps{
	  nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'target/WebApp.war', type: 'war']], credentialsId: 'nexus3', groupId: 'Demoapp', nexusUrl: '20.212.18.14:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'projectoss-release', version: "${VERSION}"
	  }
	  }
	  stage('Deploy to prod'){
		    steps{
			ansiblePlaybook become: true, becomeUser: 'azureuser', credentialsId: 'ansible', installation: 'ansible', inventory: 'ansible/hosts', playbook: 'ansible/deploy.yaml'
		}
	}
	  }
	  }
	  

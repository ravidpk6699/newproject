copyArtifacts(projectName: 'project-OSS');
pipeline {
     agent any
	   tools {
  maven 'maven3'
}
 stages{
   stage('build') {
    steps{
	  sh 'mvn clean package'
	  }
	  }
	  }
	  }

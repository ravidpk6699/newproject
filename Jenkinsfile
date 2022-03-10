pipeline {
     agent any
	   stages {
    stage('Copy Archive') {
         steps {
             script {
                step ([$class: 'CopyArtifact',
                    projectName: 'project-OSS',
                    filter: "target/webapp*.war",
                    target: 'Infra']);
            }
        }
    }
}
}

pipeline {
    agent any
    triggers {
	pollSCM('* * * * *')
	}
 
    stages {
	stage("Package") {
	     steps {
		sh "./gradlew build"
	      }
	  }
        stage("Docker Build") {
	     steps {
		sh "docker build -t mabayomi07/calculator ."
	    }
         }
	stage ("push") {
             steps {
		sh "docker push mabayomi07/calculator"
      }
}
post {
    always {
	mail to: 'dsprave5@gmail.com',
	subject: 'Completed pipeline: ${currentBUild.fullDisplayName}',
	body: 'You build completed, please check: ${env.BUILD_URl}'
	}
}
post {
    failure {
	   slackSend channel: 'dragon-teams',
	   color:	      'success',
	   message: 	      'The pipeline ${currentBuild.fullDisplayName} failed.'
	}
}

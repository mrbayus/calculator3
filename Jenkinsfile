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
}



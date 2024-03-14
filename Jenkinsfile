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
		sh "withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ])"
		sh "docker push mabayomi07/calculator"
	    }
     }
	stage ("Deploy to staging") {
	     steps { 
		sh "docker run -d --rm -p 8765:8080 --name calculator mabayomi07/calculator"
	    }
     }	
}
}


pipeline {
    agent any
    triggers {
	pollSCM('* * * * *')
	}
    environment {
	DOCKERHUB_CREDENTIALS = credentials('mabayomi07-dockerhub')
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
	stage ('Login to Docker')
	     steps {
		sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERBUNCREDENTIAL_USER --password-stdin'
            }
	}
	stage ("push") {
             steps {
		script {
		     withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ])
		sh "docker push mabayomi07/calculator"
		}
	    }
     }
	stage ("Deploy to staging") {
	     steps { 
		sh "docker run -d --rm -p 8765:8080 --name calculator mabayomi07/calculator"
	    }
     }	
}
}


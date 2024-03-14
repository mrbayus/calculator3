pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('mabayomi-dockerhub')
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
        stage ('Login to Docker') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage ("Push") {
            steps {
                sh "docker push mabayomi07/calculator"
            }
        }
        stage ("Deploy to staging") {
            steps {
                sh "docker run -d --rm -p 8765:8080 --name calculator mabayomi07/calculator"
            }
        }
	stage ("Acceptance test") {
	    steps {
		sleep 60
		sh "chmod +x acceptance_test.sh ./acceptance_test.sh"
   	    }
	}
	
	post {
	    always {
		sh "docker stop calculator"
	    }
		
	}

}

pipeline {
    agent any
    triggers {
	pollSCm('* * * * *')
	}
 
    stages {
	stage("Compile") {
	     steps {
		sh "./gradlew CompileJava"
	      }
	  }
      }

}

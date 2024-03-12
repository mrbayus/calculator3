pipeline {
    agent any 
    stages {
	stage("Compile") {
	     steps {
		sh "./gradlew CompileJava"
	      }
	  }
	stage("Code Coverage") {
	    steps {
		sh "./gradlew jacocoTestReport"
		sh "./gradlew jacocoTestCoverageVerification"
	    }
	} 
      }

}

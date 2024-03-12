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
		publishHTML (target: [
			reportDir: 'build/reports/jacoco/test/html',
			reportFiles: 'index.html',
			reportName:  'JaCoCo Report'
		])
		sh "./gradlew jacocoTestCoverageVerification'	
	    }
	} 
      }

}

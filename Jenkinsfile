#!groovy

stage ('Dev')
	milestone 1
	node {
	  echo 'Starting Pipeline Execution'

	  
	  stage ('Build-Verify') {	  
		  checkout scm		  
		  def v= version()
		  if (v) {
		  	echo "Building version ${v}"
		  }		  
		  sh 'mvn clean compile test -B verify'	  
	  }
	  
	  stage 'Build-Package' {	  
	  	sh 'mvn install deploy -Dmaven.test.skip=true'
	  }
	  def version() {
		 	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
		 	matcher ? matcher[0][1] : null
		}
	}




stage 'QA' {
	milestone 2
	echo 'unimplemented'
}


stage 'Staging' {
	milestone 3
	echo 'unimplemented'
}


stage 'Production' {
	milestone 4
	echo 'unimplemented'
}
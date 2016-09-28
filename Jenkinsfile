#!groovy

milestone 1
stage "Dev" {
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
	}
}
def version() {
 	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
 	matcher ? matcher[0][1] : null
}

milestone 2
stage "QA" {
	echo 'unimplemented'
}

milestone 3
stage "Stage" {
	echo 'unimplemented'
}

milestone 4
stage "Production" {
	echo 'unimplemented'
}
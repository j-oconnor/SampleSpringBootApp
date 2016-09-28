#!groovy

node {
  echo 'Starting Pipeline Execution'
  stage 'Build-Verify'
  echo 'Stage Build-Verify'
  checkout scm
  
  def v= version()
  if (v) {
  	echo "Building version ${v}"
  }
  
  sh 'mvn clean compile test -B verify'
  
  stage 'Build-Package'
  echo 'Stage Build-Package'
  sh 'mvn install deploy -Dmaven.test.skip=true'

 }
 def version() {
 	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
 	matcher ? matcher[0][1] : null
 }
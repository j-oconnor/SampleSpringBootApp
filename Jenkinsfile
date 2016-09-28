#!groovy

node {
  sh 'Starting Pipeline Execution'
  git 'https://github.homedepot.com/CloudEngineering/SampleSpringBootApp.git'
  sh 'ls -als'
  stage 'Stage 1'
  
  def v= version()
  if (v) {
  	echo "Building version ${v}"
  }
  withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
  	sh 'mvn -B verify'
  }
  
  stage 'Stage 2'
  
  echo 'Hello World 2'
 }
 def version() {
 	def matcher = readFile('SampleSpringBootApp/pom.xml') =~ '<version>(.+)</version>'
 	matcher ? matcher[0][1] : null
 }
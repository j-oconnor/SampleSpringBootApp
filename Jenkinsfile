#!groovy

node {
  echo 'Starting Pipeline Execution'
  stage 'Build-Verify'
  echo 'Stage Build-Verify'
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '7c71731a-52b2-4679-8369-46726bbb12fe', url: 'git@github.homedepot.com:CloudEngineering/SampleSpringBootApp.git']]])
  
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
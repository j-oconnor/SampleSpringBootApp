#!groovy

node {
  sh 'echo Starting Pipeline Execution'
  stage 'Stage 1'
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '7c71731a-52b2-4679-8369-46726bbb12fe', url: 'git@github.homedepot.com:CloudEngineering/SampleSpringBootApp.git']]])
  sh 'ls -als'
  def v= version()
  if (v) {
  	echo "Building version ${v}"
  }
  
  sh 'mvn -B verify'
  
  
  stage 'Stage 2'
  
  echo 'Hello World 2'
 }
 def version() {
 	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
 	matcher ? matcher[0][1] : null
 }
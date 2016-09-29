#!groovy

//- if test -z "$TMPDIR" ; then export TMPDIR="/tmp" ; fi
//mvn clean antrun:run@generate-properties -U
//export PROJECT=$(/usr/share/google/get_metadata_value project-id)
//export BUILD_PROPERTIES=${TMPDIR}/catalog-domain-service.properties
//export ARTIFACT_ID=`grep project.artifactId ${BUILD_PROPERTIES} | cut -d '=' -f 2`
//export GROUP_ID=`grep project.groupId ${BUILD_PROPERTIES} | cut -d '=' -f 2`
//export VERSION=`grep project.version ${BUILD_PROPERTIES} | cut -d '=' -f 2`
//export CDM_TEMPLATE_VERSION=$(curl -s https://storage.googleapis.com/${PROJECT}-bootstrap/cdm-template-version.txt)
//export CDM_TEMPLATE_VERSION=${CDM_TEMPLATE_VERSION:-v2.0.8}
//hammer --show-version

//export CONSUL_HEALTH_URI='catalog/admin/health'
//export HEALTH_CHECK_URI="/$CONSUL_HEALTH_URI"
//export HEALTH_CHECK_PORT=8080
/*
echo $PROJECT

echo $VERSION

echo $ARTIFACT_ID

echo $GROUP_ID

echo $CDM_TEMPLATE_VERSION
*/
if (env.BRANCH_NAME == 'develop') {
	stage 'Develop'
		node {		  
			stage 'Build-Compile'
				build_java()			  
			stage 'Unit-Test'
				unit_test()		  
		  	stage 'Package-Upload' 	  
		  		package_upload()
		}
} else if (env.BRANCH_NAME == 'stage') {
		stage 'Stage'
		node {
			echo 'Stage unimplemented'
		}
} else {
	//feature

}
	
def build_java() {
	checkout scm
	sh 'mvn clean compile'	
}

def unit_test() {
	sh 'mvn test -B verify'
}

def package_upload() {
	sh 'mvn install deploy -Dmaven.test.skip=true'
}

def version() {
	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
	matcher ? matcher[0][1] : null
}
